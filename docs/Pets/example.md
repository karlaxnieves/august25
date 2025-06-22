---
title: example
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Release 1924.1 (11/22/2019)

The following items are slated for AppCloud Release 1924.1:  
**End User Features/Changes**

- **Enhancement: Copy/Paste Support** The new Talking Points Recommendation Creator/Updater app now allows more robust copy/paste support from Microsoft applications including MS Word and MS OneNote. When pasting from Microsoft applications, you can still keep or clean content but now can drag/move field merges into content, bullets, etc.

## Release 1923.2 (11/15/2019)

The following items are slated for AppCloud Release 1923.2:  
**End User Features/Changes**

- **New Feature: Content Library.** A new Content Library, accessible via the Eloqua Cloud menu, allows users to create dynamic content using rules that can be added to the new Talking Points Recommendations Creator/Updater app.
- **New Feature: Talking Points Recommendation Creator/Updater App.** To streamline Eloqua program flows, a new Talking Points Recommendation Creator/Updater app has been released with a new content editor. The new editor provides more formatting options, allows for better management of data mart and Eloqua field merges, and enables Content Library content. The new app also provides a single step for both creating new, if the record does not have a Salesforce.com Recommendations record, or updating existing Recommendation records.
- **New Feature: Global Scheduling.** A global default schedule has been added to the app setup area allowing app admins to set or update the run time for any active Play Builder feeder. Play Builder users have the option, within the Play Builder feeder app, to override the global schedule.

![2940](https://files.readme.io/d4f4bdd-tfs-playbuilder-schedule.png "tfs-playbuilder-schedule.png")

## Release 1915.3 (07/26/2019)

The following items are slated for AppCloud Release 1915.3:

**End User Features/Changes**

- **New Feature: Supporting Simple Pipe Delimited Concatenated Fields for Talking Points Action.** The Talking Points Creator and Talking Points Updater apps will now automatically generate bullet lists for pipe-delimited fields. A Pipe Delimited field appears as a darker green merge field (e.g., Gap-TalkingPoints):

<Image title="TFS-PipeDelimited.png" alt={1000} border={true} src="https://files.readme.io/d7dd171-TFS-PipeDelimited.png">
  Darker green merge field indicates a pipe delimited field.
</Image>

<Image title="TFS-PipeDelimited_sfdc.png" alt={2026} border={true} src="https://files.readme.io/5c9c5b5-TFS-PipeDelimited_sfdc.png">
  Pipe delimited layout within Salesforce.com.
</Image>

- **New Feature: Field Merge Groups for Talking Points Action.** To better support large numbers of merge fields, fields are now grouped together. Additionally, data mart merge fields are displayed above Eloqua merge fields. 
- **New Feature: Vendor Fields Added to Sales History Criteria.** Vendor options, including a type-ahead search for Vendor Name/Number, Self Manufacture and SSP Options have been added to the Sales History criteria.

<Image className="border" border={true} src="https://files.readme.io/2376c53-TFS-VendorFields.png" />

- **New Feature: Localized Currency.** Currency fields available as field merges for the Talking Points Creator and Talking Points Updater apps now include the currency symbol and formatting based on an Account's language and location.
- **New Feature: Salesforce.com Recommendation ID Now Global Field.** The Salesforce.com Recommendation ID field has been removed from the Talking Points Creator and Updater apps and moved into the app settings area.
- **New Feature: Updated Numeric Formatting.** Numeric and Integer field merge values will now be written to Salesforce.com in standard form (non-scientific notation).

**Backend Features/Changes**

- **Enhancement: Support for Multiple Divisions.** The API used to access information from the Thermo Fisher Redshift data warehouse now supports more than one division by introducing a division header that can be added within the app setup area.

- **Enhancement: Amazon SQS Message Visibility Timeout.** To improve overall system performance and messaging queueing, visibility timeouts were updated for the following queue listeners:

  - EloquaExporterQueueListener
  - EloquaImporterQueueListener
  - ExecutionQueueListener
  - TalkingPointsRecommendationQueueListener
  - TalkingPointsRecommendationUpdaterQueueListener
  - TfsDataMartQueryListener 

- **Enhancement: Reduce Eloqua 401 Messages.** The OAuth gatekeeper queuing was updated to reduce concurrent requests for Eloqua OAuth token refreshes.

## Release 1912.2 (06/12/2019)

The following items are slated for AppCloud Release 1912.1:

**End User Features/Changes**

- **New Feature: Supporting All Values for a CMT Level.** The Play Builder will now allow users to select a specific value for CMTs 2-8 OR leave the value blank and return all values for the desired CMT level.

- **Enhancement: Eliminate Issues When Using Special Characters.** This enhancement makes a global backend encoding change for the Talking Points Creator and Talking Points Updater apps to prevent special characters (e.g., emDash) being converted to ? or other unexpected values in Salesforce.com. All existing configurations will have this change applied - no user action needed.

**Backend Features/Changes**

- **Enhancement: Update RDS Postgres ETL Table On All Events.** To ensure the RDS Postgres table used to store Eloqua Feeder information (Play Builder), a backend change was made to update the information on the following events: 
- On Eloqua Program activation/pause/unpause/deactivation
- When saving the feeder configuration IF the number of criteria has changed, if the query criteria have changed or if there is a change in criteria types
- **Enhancement: Update External Processor to Prevent SQS Listener Starvation.** The AWS SQS queues have an unnecessary limit to the maximum messages allowed on the queue causing the External Processor to reject new messages once the thread pool has hit its maximum limit. This change increased the SQS queue capacity of all ThreadPoolTaskExecutor configurations to 20,000 (the maximum number for an SQS FIFO queue) and also increases maximum thread pool sizes to 100-200 for listeners, depending on listener type (NOTE: we will continue to monitor the thread pool size against EC2 performance and adjust as needed going forward).
- **Enhancement: Update EP Database Connection Pool.** To prevent EP database connection starvation, we have increased the connection pool for the EP database to 100.
- **Enhancement: Increase AWS SQS Invisibility Timing.** When importing data into Eloqua we noticed some slower than expected response times. We have increased the message invisibility timing to 2 minutes (up from the standard 30 seconds) to prevent the same message from being unnecessarily reprocessed. 
- **Enhancement: Increase Record Processing Speed by Switching to Bulk Updates to Internal Database.** When processing data, we now update record status in bulk, instead of record-by-record, based on the Eloqua execution ID and record notification size.

<HTMLBlock>{\`

<div></div>
<hr>
<style></style>
`}</HTMLBlock>

## Release 1910.2 (05/17/2019)

The following items are slated for AppCloud Release 1910.2:

**End User Features/Changes**

- **New Feature: Sales Play Builder Ongoing Feeder** - the Sales Play Builder will now allow users to optionally enable an ongoing feed of records into the Eloqua Program Canvas. 

<Image className="border" border={true} src="https://files.readme.io/4ac48a1-tfs_feeder_ongoing.png" />

When enabled, the Play Builder query will be executed against the Data Warehouse once every 24-hours from the time the Canvas is Activated or Reactivated or if the toggle is enabled when saving the Play Builder configuration on an Activated Program Canvas. If you deactivate and reactivate your Canvas, the Play Builder will run immediately and then reset the schedule to once every 24-hours based on the new reactivation timestamp.

- **New Feature: Publish Play Builder Query Information to RDS** - to support the ETL processes build created to keep records updated in Salesforce.com, this new feature will publish Play Builder query information to a AWS RDS database. Values include Instance ID (unique identifier), Eloqua Program ID, Segmentation Query, Is Ongoing, Date Created, Date Last Modified, Status, and Last Status Date. This change will also allow the Play Builder ID (Instance ID) to be be mapped to the Salesforce.com Recommendation record.

- **Bug Fix: Odd characters in the Talking Points Creator app when using the hyperlink tool within the Talking Points editor being translated as question marks (?) in Salesforce.com.** This fix removes the special characters that were being added in the HTML which caused the Talking Points field in Salesforce.com to have extra questions marks around a link.

<HTMLBlock>{\`

<div></div>
<hr>
<style></style>
`}</HTMLBlock>

## Release 1910.1 (05/13/2019)

The following items were included in AppCloud Release 1910.1:

**End User Features/Changes**

- **New Feature: Talking Points Updater** - New Cloud Action app that allows updates to an existing  Salesforce.com Recommendation record including:
  - Play Name
  - Play Description
  - Hot Play
  - Talking Points content (including field merges)

- **Bug Fix: Inconsistencies in Drag/Drop of field merges on the Talking Points editor.** This was caused by trying to drag merge fields into HTML a <div> area which isn't allowed and causes the merge fields to visually "bounce" back to the right-hand field list area. The HTML structure was updated so it does not include those nested <div> areas. Please keep in mind, older configurations created prior to this fix will still work when being processed for record creation but my have this "bouncy" behavior. If this happens, the content for the Talking Points should be deleted and recreated and the configuration saved (per training notes).

<HTMLBlock>{\`

<div></div>
<hr>
<style></style>
`}</HTMLBlock>

## Release 1910 (05/07/2019)

The following items were included in AppCloud Release 1910:

**Backend Features/Changes**

- **Bug Fix: OAuth token not getting refreshed after 24-hour expiration period.** An expired OAuth token between the Runner-TFS system within the Relationship One AWS environment and the External Processor (Thermo Fisher AWS environment) now gets refreshed when a request is made.
- **Bug Fix: Eloqua Program ID is not being included in the system generated uinque ID.** The Sales Play Builder settings allow a user to use a Data Mart field or a system-generated unique ID, which is a concatenation of the Eloqua Program ID and the Data Mart ID, when importing data into an Eloqua Custom Data Object. This fix populates the Eloqua Program Eloqua Program ID portion of that unique identifier.
- **Improvement: Add logentries logging to the External Processor.** To help with support and system monitoring, system logs from the External Processor will be added to the Relationship One logentries system.