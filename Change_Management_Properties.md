# Change Management Properties
## Customization Properties for the Change Management Module

1. Change Request Tasks approval engine:
- Process Guides

2. Change Risk calculation method. Business Rule calculates on insert/update, UI Action calculates only on demand. None disables this capability.
- UI Action

3. Enable Copy Change feature
- Yes

4. List of attributes (comma-separated) that will be copied from the originating change
- category,cmdb_ci,priority,risk,impact,type,assignment_group,assigned_to,short_description,description,change_plan,backout_plan,test_plan

5. Copy attachments from originating change
- Yes

6. List of attributes (comma-separated) from Change Task (change_task) related list that will be copied from the originating change
- cmdb_ci,priority,assignment_group,assigned_to,short_description,description

7. List of attributes (comma-separated) from Affected CIs (task_ci) related list that will be copied from the originating change
- ci_item

8. List of attributes (comma-separated) from Impacted Services (task_cmdb_ci_service) related list that will be copied from the originating change
- cmdb_ci_service

9. Show an information message when a change schedule is pinned
- Yes

10. Configures how Discovery will be triggered for Affected CIs (automatically, manually or off)
- off

11. List of Change Request states (comma-separated) where Discovery can be triggered manually
- Implement, Review

12. List of Change Request states (comma-separated) where Discovery will trigger automatically. E.g. when the Change Request's state changes to Review
- Review

## END

