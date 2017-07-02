---
layout: post
title: '200 Records: Understanding The Limit'
date: '2015-01-04 19:53:22'
tags:
- limits
- salesforce
- triggers
- apex
---

#### 200 Records and Transactions

When you update a single record in Salesforce, the before update and after update triggers on the object both run once to process the record with the custom logic defined in your organization. The trigger collection only contains the one record that was updated.

When you update 200 records using the Data Loader or the API, the exact same triggers run. This time the trigger collection contains 200 records.

As it is the same code that runs for single or bulk operations all apex trigger code must be written expecting the bulk scenario.

Many of the Salesforce limits are based around the concept of a transaction. A transaction is an execution context on the Force.com platform. When you update 200 records this is done within one context. If you update 201 records through the Data Loader then this is done over two contexts and these two transactions are entirely separate.

The above is widely understood in the Salesforce community and is well documented in the DEV501 course. Everyone knows that you shouldn't put SOQL queries within loops. 

#### Triggers from DML Scenario

What's less well understood is what happens when you perform DML operations on other objects in your triggers (or classes), and cause the triggers on the second object to run too. Let's illustrate how it works with an example, e.g. you have this requirement:

> You want to be able to mark an account as inactive and this to cause all the related contacts to be set to inactive. 

(Let's say for this example you can't use a formula field on contacts to do this because you need to use this in a criteria based sharing rule which can't use a formula)

#### Investigation of Behaviour

We add an Active\_Checkbox__c custom checkbox field on account and contact (default value true) and then we put something like the following in the account after update trigger:

(Note all the code from this post is available in this [gist](https://gist.github.com/samdavyson/ef3972bf973d9a211698))

<script src="https://gist.github.com/samdavyson/ef3972bf973d9a211698.js?file=AccountTrigger.cls"></script>

Now we add a Batch\_Size__c custom text field to the contact and add this logic to the before update trigger:

<script src="https://gist.github.com/samdavyson/ef3972bf973d9a211698.js?file=ContactTrigger.cls"></script>

If the organization has 200 accounts, all of which are active (Active__c = True) and each account has 40 contacts. When we update the 200 accounts we would expect the trigger to update 200 x 40 = 8,000 records. 

Lets add a static class to count the number of times this trigger runs:

<script src="https://gist.github.com/samdavyson/ef3972bf973d9a211698.js?file=runCounter.cls"></script>

 We can put this in the contact trigger:

<script src="https://gist.github.com/samdavyson/ef3972bf973d9a211698.js?file=ContactTrigger.cls"></script>
    
#### The Test
So now everything is prepared. We can try to deactivate 200 accounts by running this in Execute Anonymous:

<script src="https://gist.github.com/samdavyson/ef3972bf973d9a211698.js?file=execAnon.cls"></script>
    
So now we expect 8,000 contact records to be updated. Are these updated in bunches of 200 records also?

#### The Results
Yes they are. After running the code above the batch size is set to 200 on all contact records that were updated and the contact trigger has run 40 times.

The key point is that although this batching has occured into groups of 200, all of the groups of 200 ran in **one transaction**. And one transaction means one set of limits. 

> This effect can mean you go unexpectedly close to the limits for SOQL queries or @future calls. 

For instance in your contact trigger you performed two SOQL queries outside of the contacts loop, then you would have used 2 x 40 = 80 SOQL queries in the transaction. The limit is currently 100.

Or if you have two @future calls in your contact trigger, this would use 80 future calls. The limit is currently only 50, so this would throw a limit exception.

#### Summary
Triggers always process records in batches of 200 regardless of how they are called: API, other triggers, classes etc.

> If you are updating many records from DML then remember the **whole trigger will run multiple times**, so properly bulkified code can still hit the limits. 

This problem common if changing something on the Master record in a Master-Detail relationship causes all Detail records to update.

The best solution is to build your Salesforce customisations holistically and to carefully think through the impacts that updating many records in a DML statement can have.

Photo: [countylemonade](https://www.flickr.com/photos/countylemonade/5916416464), Code: [Github Gist](https://gist.github.com/samdavyson/ef3972bf973d9a211698)
   