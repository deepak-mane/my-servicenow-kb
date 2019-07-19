# Today's post is going to talk about a few hidden features in Service-Now that will save you time. 

Navigation filter
The Navigation filter is the search box above the navigation pane. The default behavior is to filter the navigation list to help you quickly find different applications and modules. 

If you type a table name in the navigation filter, for example incident, it will start to filter the modules and applications. If you add .list (incident.list) to the end of the table, it will return a list of records in that table. If you capitalize LIST it will give you the same list in a new window.

You can also do the same with .form (incident.form) and also .FORM which will return the default form for this table. 
 Reference fields
Reference fields are used to reference a different table in the system. An example of this is the "Assigned To" field on the "Incident" table, which stores your companies users. The default behavior is to search the records with a "STARTSWITH" query. If you are looking up Michael, you may be required to type the full name before you get the right Michael. 

The hidden feature here is the asterisks and double asterisks. If you use an asterisks before you start typing it will change the query to a CONTAINS search and allow you to search by last name. 

If you use double asterisks it will quickly return the first 15 records in the table.


Generating Encoded Queries
Encoded Queries are documented on the Service-Now wiki but I want to walk you though how to generate the Encoded Query for use with a GlideRecord look-up.

The use case we will use today is, incident clean-up. If an incident has been open for longer then 120 days we want to automatically close it.

First step will be to get our encoded query, to do this we will need to open a list of incidents. We can use the Navigation filter by typing incident.list.

Once the list comes up,  we will want to filter for only incidents that are active and created before 120 days.

Next we will want to right click the link and Copy Query


You should receive a pop-up with the Encoded Query inside, if you do not, it may be that it is already in the clipboard. 

Finally you will want to write your script.

You can now take your script and copy it into a Scheduled Job for execution. 

Always test in non-production!!!
Ninja update
So we just closed 18 incidents in the last example and 18 emails went out to let people know we closed the incidents. Now this may not seem like a big deal but imagine you were updating 500 incidents or even 1,000.

To prevent emails in the future we could have called two methods in our GlideRecord object to prevent emails from being triggered and system fields from being updated. Those methods are "setWorkflow(false)" and "autoSysFields(false)".

The first method, setWorkflow(false), will prevent any Business Rules or Workflows from running on the record during the update.

The second method, autoSysFields(false), will prevent any system fields from being updated, Updated By, Updated, etc. 

Here is our updated script.

Thank you for taking the time to read. If you have any feedback please reply in the comments field. 
