# SLA Engine Properties
You are using the 2011 SLA engine and the configurable properties for this engine are displayed below

[Click here to view the online help](http://docs.servicenow.com/?context=CSHelp:SLA-Engine-Properties)

Percentage at which scheduled jobs stop refreshing Task SLA timings
Maximum 'Actual elapsed percentage' value after which the 'SLA - update calculations' scheduled jobs will stop regularly calculating a Task SLA's time values.
This is typically used to prevent 'long since breached' records from being unnecessarily updated.
Default is 1000. Set to 0 to stop all calculations and leave blank to enable calculation of all task SLAs.
1000


Execute the 2011 SLA engine asynchronously
Set to Yes to create a scheduled job to run the SLA engine when a task is created or updated (Note: This results in a slight delay in the Task SLA records being created and updated).
Set to No to run the SLA engine synchronously when a task is inserted or updated and thus make it visible immediately.
Yes | No

Enable compatibility with 2010 'breached' stage for SLAs
Set to yes to set a Task SLA's stage field to breached when it exceeds the breach time
Note: this is legacy behaviour as the 2011 engine sets the Has breached field to indicate that a Task SLA has exceeded the breach time
Yes | No

Default condition type
Enter the name of the script include used to evaluate SLA Conditions for the 2011 SLA engine. You can use this to override with your own extension of the SLAConditionBase script include.
For more information on condition types click here.
SLAConditionBase


Run workflow for a Task SLA that is already breached when it attaches
Set to Yes to ensure that the workflow for a Task SLA is executed when the Task SLA is already breached when it is attached to the task.
Yes | No

Use Business time left field to determine if an SLA is breached
Set to Yes to ensure the value of the Business time left field on a Task SLA is used to determine if it has breached.
Set to No to ensure the value of the Business percentage field is used to determine if it has breached.
Note: The percentage value is rounded to 2 decimal places, such as 99.51% rounded to 100%, which may lead to a Task SLA being incorrectly set to have a breached status.
Yes | No

Refresh Task SLAs when a Task form is displayed
Select Yes to ensure that the timings in the Task SLAs are updated each time the task form is viewed.
Yes | No

Always populate business fields on a Task SLA
Set to No to leave the "business" fields empty or at 0 if a Task SLA does not have a schedule.
Set to Yes to ensure that the "business" fields will contain the same values as those in the "actual" fields when the Task SLA does not have a schedule.
Yes | No

Conditions in SLA Definitions are case-sensitive
Set to Yes if you want the SLA engine to perform a case-sensitive match when checking an SLA Definition's conditions
Set to No if you want the SLA engine to perform a case-insensitive match when checking an SLA Definition's conditions
Yes | No
