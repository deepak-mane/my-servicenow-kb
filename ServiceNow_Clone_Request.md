# ServiceNow Clone Instances

## System clone
The system clone application allows users with the clone_admin or admin role to clone data from one instance to another.

This functionality is primarily used to clone a production instance over an existing sub-production instance before developing or testing changes. All clones are performed using the most recent nightly backup.

In response to a clone request, the ServiceNow platform performs the following tasks:
1. Generates a file to preserve operational data on the target server.This file contains the data preserved by data preservers.
2. Copies the database schema from the source instance to the target instance.
3. Creates tables in the target instance database using the source instance table definitions.
4. Copies data from the most recent nightly backup of the source instance to the target instance database. Certain large tables are normally excluded. These include audit, log, and email tables.
5. Briefly disables UI traffic and requests to the target instance server.
6. Displays the message Clone in progress... to any user accessing the target instance.
7. Restores operational data preserved from the target instance.
8. Runs any post-clone cleanup scripts on the target instance.
9. Briefly suspends all email functions on the target instance.
10. Queues an event to regenerate text indexes.
11. Enables UI traffic and requests to the target instance server.

During a clone, the target instance may be intermittently unavailable. After clone completion, you have up to 24 hours to contact ServiceNow Customer Support and request a rollback of the target instance to its pre-clone state. You are notified when the rollback is complete.

- Clone to an instance on a different version :The System Clone application can target an instance running a different instance version from the source. A central web service controls clone processing and automatically modifies the target instance version to match the source instance version. This matching process starts up to 8 hours before the time specified in the Date and time field on the System Clone form. This web service also ensures that there is enough disk space on the target instance for the clone to proceed. When cloning from a backup, the target instance does not need additional time to upgrade or downgrade. The ServiceNow platform performs any version changes during a brief window where the target instance is unavailable, after it copies data from the source instance backup.

- Clone from a backup :The platform uses data from the most recent nightly backup of the source instance when cloning. Backups used for cloning are at most 36 hours old. System Clone begins the initial preparation process, including selecting the latest backup to use, only at the date and time processing is scheduled to commence.

- Clone over production instances:Production instances cannot be used as the target instance for a clone after the instance is live.

### Request a clone
Request a clone to copy data from a production instance to a non-production instance, or to copy data between non-production instances.
- Procedure
 1. Create a clone target record for each target instance you want to receive clone data.
 1. Verify the list of tables excluded from cloning and add or remove tables to exclude from the target instance.
 1. Verify the list of tables and system properties that will be saved on the target instance by data preservers and create or modify data preservers as needed.
 1. The legacy clone engine does not support data preservers for these records.
 1. Tables that extend Task
 1. Relationships
 1. Hierarchies
 1. Dot-walked queries
 1. If you are preserving any data not supported by the legacy clone engine, verify there is a recent backup of the target instance available. Should the clone-from-backup-process fail for any reason, you can restore the target instance from the backup.


#### Create a clone target
A clone target record specifies the instance URL and credentials used for cloning.

#### Exclude a table from cloning
Exclude a table to create an empty but usable table on the target instance.

#### Data preservation on cloning target instances
Data can use data preservers to protect data on the target instance from being overwritten. If you have custom applications, you must also manually preserve unpublished application content.

Preserve any unpublished applications on the target instance.
Navigate to System Clone > Request Clone.
Select the Target instance to receive the cloned data.
You must create a separate clone request for each target instance you want to receive clone data.
Complete the Options form section.
Data preservation on cloning target instances
  - Data preservers : Consider whether to preserve the data in the following tables.
   - Bookmark [sys_ui_bookmark]
   - Recent Selection [sys_ui_recent_selection]
   - User Preference [sys_user_preference]
  - Do not use data preservers to transfer large sets of data, such as user groups. If you must preserve table data such as users, groups, and roles, consider exporting the records to a file and importing it after the clone is complete.
  - Data preservers for Multi-SSO
  - Data preservers for SAML
  - Preservation of unpublished applications
  - Create a data preserver :
   - Procedure : 
    - On the source instance, navigate to System Clone > Preserve Data.
    - Click New.Enter the table label as the Name, for example, User Preference for the [sys_user_preference] table.
    - Select the Table to be preserved. Select the Theme check box if the data being preserved is a UI property.
    - Define the data to be preserved using the Condition Builder .Click Submit.
    - If you want to delete the data preserver later, make sure not to modify or delete the following data preserver records:
     - Core Instance Properties
     - Semaphores
     - Email Accounts
   - If you set a data preserver on a table where the source instance has more records than the target instance, the data preserved on the target instance also includes the additional records from the source instance. 
   - To resolve this issue and to preserve only the records in the target table, create an exclude table record for the target table, in addition to setting the data preserver on the source table.
  - Preserve SAML properties
  - Preserve unpublished applications during a system clone

### Cancel a clone
  - Navigate to System Clone > Live Clones > Active Clones. The system displays the list of currently active clones.
  - Select the clone you want to cancel. The system displays the System clone record.
  - From Related Links, click Cancel Clone. The system stops any current clone activities and sets the State to Canceled.
  - If you want to restart a canceled clone, click Restart Clone, otherwise you can create a new clone request.
  
### View clone history
  - Navigate to System Clone > Live Clones > Clone History.
  
### Post-clone cleanup scripts
  - To add a script, navigate to System Clone > Clone Definition > Cleanup Scripts and click New.

|Script	| Description |
| --- | --- |
|Bad MID Server credentials after clone	|Runs a script include called BadMIDCredentialAfterClone on a cloned instance to detect bad MID Server user credentials. This script include creates scheduled jobs that log MID Servers in the Down state to the MID Server Issue [ecc_agent_issue] table after an instance clone.
|Clear scheduled job node association	|Resets any scheduled jobs that were active on the source instance to the Ready state. This script also clears the value of the System ID and Claimed by fields on all scheduled jobs.
|Configure Email Accounts	|Migrates email accounts that existed on the source instance to the target instance if they are not enabled there. This script also migrates the email properties to the target instance.
|Disable emails	|Disables email on the target instance. A default data preserver maintains other email settings from the target instance.
|Install deactivated plugin|	Enables the Domain Separation plugin for instances that use this feature.
|Regenerate all text indexes|	Rebuilds text indexes on the target instance after a clone. Text indexes are not cloned from the source to the target instance.
|Schedule drop backup tables|	Schedules the deletion of the data contained in the target instance database prior to the clone. This original data is preserved for 24 hours following a clone to allow you to roll back an instance to the pre-clone state. If the target instance is downgraded as part of the clone, backup data is not available.
