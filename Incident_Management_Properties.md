# Incident Management Properties
## Incident closure properties
1. Enable auto closure of incidents based on Resolution date. Setting this to 'No' will make auto closure to run based on the Updated date.
Yes
2. Number of days (integer) after which Resolved incidents are automatically closed. Zero (0) disables this feature.
10
3. Close open Incident Tasks when Incident is closed or canceled.
Yes
4. Close open Incident Communication Plans when Incident is closed or canceled.
No
5. Close open Incident Communication Tasks when an Incident Communication Plan is closed or canceled.
No

## Incident Re-open Properties
List of fields (comma-separated) to copy from the original incident when an incident is reopened by email.
additional_assignee_list,
assignment_group,
business_service,
caller_id,
category,
cmdb_ci,
company,
description,
group_list,
impact,
knowledge,
location,
parent,
parent_incident,
priority,
problem_id,
rfc,
severity,
short_description,
subcategory,
urgency,
watch_list

## Copy Incident and Create Child Incident Properties
Enable copy incident feature
Yes

Enable create child incident feature.
Yes

Copy attachments from originating incident
Yes

List of attributes (comma-separated) that will be copied from the originating incident
assignment_group,
business_service,
category,
caused_by,
cmdb_ci,
company,
description,
impact,
location,
parent_incident,
problem_id,
rfc,
short_description,
subcategory,
urgency,
priority,
u_issue_type

Related lists (comma-separated) that will be copied from the originating incident
task_ci,
task_cmdb_ci_service

List of attributes (comma-separated) from Affected CIs (task_ci) related list that will be copied from the originating incident
ci_item

List of attributes (comma-separated) from Impacted Services (task_cmdb_ci_service) related list that will be copied from the originating incident
cmdb_ci_service

## Incident Form Fields Configuration Properties

Incident activity formatter fields
assigned_to,
cmdb_ci,
incident_state,
impact,
priority,
opened_by,
work_notes,
comments,
*Email*,
*Relations*,
*Attachments*,
close_code,
close_notes,
actions_taken,
category,
caller_id,
subcategory,
u_issue_type,
u_actual_start_date,
state,
hold_reason,
contact_type,
assignment_group,
urgency,
short_description,
watch_list,
parent_incident,
caused_by,
knowledge

Additional comments icon used in Task Activity formatter.
images/icons/edit.gifx
Lookup image using list

Work notes icon used in Task Activity formatter.
images/icons/filters.gifx

Incident additional comments style.
background-color: WhiteSmoke

Incident work notes style.
background-color: LightGoldenRodYellow

