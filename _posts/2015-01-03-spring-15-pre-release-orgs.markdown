---
layout: post
title: Spring '15 Pre-Release Orgs
date: '2015-01-03 17:17:19'
tags:
- salesforce
- pre-release
- spring15
- new-features
---

The Spring '15 pre-release orgs are available. You can sign up for one by filling in [this form](https://www.salesforce.com/form/signup/prerelease-spring15.jsp).

I have briefly looked around. Here are the points highlighted as new in the setup menu:

##### User Success Journeys

> Salesforce User Success Journeys guide users with customized suggestions based on how they use Salesforce and the Salesforce1 mobile app. Help your users succeed with tips on actions they can take to accomplish more—faster.

Note that this is currently available for US organizations only.

##### Named Credentials

![Named Credentials UI](/assets/images/Screenshot-2014-12-31-17-52-27.png)

> A named credential specifies a callout endpoint and its required authentication parameters. When setting up callouts, avoid setting authentication parameters for each callout by referencing named credentials.

##### Clean Rules

> Clean rules control the clean process by defining which Salesforce records to clean and how to clean them. Each clean rule specifies the:

> * Data service used to clean records
* Salesforce records that are cleaned
* Fields affected by the cleaning

> For example, you may have a clean rule that uses the Data.com Social Key data service to enrich social profile fields for Contact records.

##### Duplicate Management

![Account Matching Rule UI](/assets/images/Screenshot-2014-12-31-17-33-13.png)

> Duplicate Rules work together with matching rules to prevent users from creating duplicate records.

> Matching Rules determine whether the record a user is creating or updating is similar enough to other records to be considered a duplicate, whereas duplicate rules tell Salesforce what action to take when duplicates are identified.

> For example, a duplicate rule can block users from saving records that have been identified as possible duplicates, or simply alert users that they may be creating a duplicate, but allow them to save the record anyway.

> For complete implementation information, download [Managing Duplicate Records in Salesforce](https://gs0.salesforce.com/help/doc/en/salesforce_data_quality_duplicate_prevention.pdf).

##### Sales Paths

![Sales Path In Setup Menu](/content/images/2015/01/Screenshot-2014-12-31-17-35-27.png)

![Sales Path Step 1](/content/images/2015/01/Screenshot-2014-12-31-17-34-22.png)

![Sales Path Step 2](/content/images/2015/01/Screenshot-2014-12-31-17-34-35.png)

> Give your sales reps a visual guide in the Salesforce1 mobile app: Show them where they are in the sales process and what they need to do next to close the sale. Have multiple sales processes at your company? Create a Sales Path (one per record type) for each process.

> * Each Sales Path you create displays the key fields for sales stages on opportunity records.
* Help reps nail their deals with guidance for success—information and links that you create for each stage.
* Each Sales Path you activate is automatically added to the page layout for that record type.

This functionality has been created with the Aura framework.

##### Assets

Record types and sharing for Assets.

##### Salesforce Files

![Regenerate Previews for Files](/assets/images/Screenshot-2014-12-31-17-40-54.png)

Regenerate previews for Salesforce Files.

##### Action Link Templates

> Use action link group templates to instantiate action link groups with common properties.

> An action link is a button on a feed element that targets an API, a Web page, or a file. Use action links to integrate Salesforce and third-party systems into the feed. Every action link belongs to an action link group and action links within the group are mutually exclusive.

Is there anything else new that you have spotted?