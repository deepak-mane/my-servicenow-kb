# ServiceNow Clone Instances


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

Cancel a clone
  - Navigate to System Clone > Live Clones > Active Clones. The system displays the list of currently active clones.
  - Select the clone you want to cancel. The system displays the System clone record.
  - From Related Links, click Cancel Clone. The system stops any current clone activities and sets the State to Canceled.
  - If you want to restart a canceled clone, click Restart Clone, otherwise you can create a new clone request.
View clone history
  - Navigate to System Clone > Live Clones > Clone History.
Post-clone cleanup scripts
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
