# Export Data from ServiceNow



### To export data directly from the URL, create a URL containing the following parts:
- Procedure
1. Specify the instance URL. For example, https://<instance name>.service-now.com/.
2. Specify the table form or list to export. For example, incident_list.do.
3. Specify the export format processor to use for the export. For example, ?CSV.
4. (Optional) Specify a query and sort order with URL parameters. For example, &sysparm_query=sys_id%3E%3Db4aedb520a0a0b1001af10e278657d27.

The final URL should look like one of these sample URLs:
URL	Description
https://<instance name>.service-now.com/incident_list.do?CSV	Export all incidents to a comma-separated value text file.
https://<instance name>.service-now.com/incident_list.do?CSV&sysparm_query=sys_id%3E%3Db4aedb520a0a0b1001af10e278657d27	Export a particular incident to a comma-separated value text file.
https://<instance name>.service-now.com/incident_list.do?CSV&sysparm_orderby=sys_id	Export all incidents to a comma-separated value text file and sort the list by sys_id.
