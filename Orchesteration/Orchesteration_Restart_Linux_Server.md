# Orchestration Example - Restart a Linux Server
```
 Contents
1	Overview
2	Design Summary
3	Add the Role
4	Create the UI Action
5	Create the Orchestration Workflow
5.1	Refining the Workflow
```

### Overview
This example demonstrates how to create an Orchestration workflow that allows an authorized helpdesk user to restart a Linux server from a UI Action on an incident form.

### Design Summary
This exercise involves the following procedures:

### Create a role that authorizes helpdesk personnel to restart a Linux server.
Add a UI Action to the Incident form that appears for authorized users when the incident involves a Linux server
Create the Orchestration Workflow, triggered by the UI Action, that restarts the server and logs the results to the incident.
Add the Role
Navigate to User Administration > Roles.
In the list of existing roles, click New.
Use rebooter as the Name of the role and type a description, such as, Helpdesk technician authorized to restart servers using Orchestration.
Click Submit.

RBA_Example_Role.png

### Create the UI Action
Navigate to Incident > Open.
From the list of incidents or from an incident record, right-click in the header bar, and select the appropriate option for your version:
Fuji or later: Configure > UI Actions
Eureka or earlier: Personalize > UI Actions
Click New in the list of UI Actions.
In the UI Actions form, type the Name of the UI Action as it should appear in the link.
For this example, we enter Restart Linux Server.
Select the Form Link check box.
Create the UI Action Condition.
For this example, we enter:
<source lang="javascript">gs.hasRole('rebooter') && current.cmdb_ci && current.cmdb_ci.sys_class_name == 'cmdb_ci_linux_server'</source>
This condition evaluates the following:
The first term restricts the UI Action to users with the rebooter role.
The second term requires a CI. This prevents an error when evaluating the third term if there is no CI reference.
The third term requires this CI to be a Linux server.
Create the following UI Action Script, and then click Submit.
```
<source lang="javascript">var gr = new GlideRecord('wf_workflow');

 gr.addQuery('name', 'Restart Linux Server');
 gr.query();
 if (gr.next()) {
  var wf = new Workflow();
  var workflowId =  + gr.sys_id;
  var vars = {};
  wf.startFlow(workflowId, current, current.operation, vars);
 }
 action.setRedirectURL(current);</source>
```
This script does the following:
  Locates the Orchestration workflow by name.
  Starts the workflow.
  Redirects back to the incident.
  
The UI Action form looks like this:

Error creating thumbnail: Unable to save thumbnail to destination
Create the Orchestration Workflow
For instructions about using Workflows, see Graphical Workflow Editor.

Navigate to Orchestration > Workflow Editor, and then click New.
Enter the name for this Workflow that matches the UI Action created in the previous procedure. In this case, type Restart Linux Server.
Select Incident [incident] as the Table.
Select None in the If condition matches field.
This workflow is started from a script and not a condition.
Enter a description of the workflow in the Description field.

Error creating thumbnail: Unable to save thumbnail to destination

Click Submit.
The beginning Workflow appears.

Error creating thumbnail: Unable to save thumbnail to destination

Drag the Run Command activity from the Orchestration heading in the palette on the right on to the transition line between the Begin and End points.
In the Run Command activity form, type a Name for the activity, such as shutdown and reboot.
Add a hostname or IP address, in this case the scratchpad variable, ${workflow.scratchpad.ip}.
This variable contains the IP address of a target CI in an incident, which is discovered by a script run in a Run Script activity (added next). Any IPv4 address that points to a NIC that points to the same CI in the target incident will work.
Type shutdown -r now in the Command field.
This is the shutdown command that is run on the target CI using the IP address provided by the scratchpad variable.

Error creating thumbnail: Unable to save thumbnail to destination

Click Submit.
The Run Command activity appears in the Workflow.

Error creating thumbnail: Unable to save thumbnail to destination

Drag the Run Script activity from the Utilities palette to the transition line between the beginning of the Workflow and the Run Command activity from the previous step.
In the Run Script activity form, type a descriptive Name, such as Get IP address.
Add the following script to the Script field to return the IP address of the target CI, and then click Submit:
<source lang="javascript">// find IP address by querying for IPs associated with NICs

 // that are associated with our Linux Server CI
  var gr = new GlideRecord('cmdb_ci_ip_address');
  gr.addQuery('ip_version', '4');
  gr.addQuery('nic.cmdb_ci',  + current.cmdb_ci);
  gr.query();
  if (gr.next()) {
    activity.result = "success";
    var ip =  + gr.ip_address;
    workflow.scratchpad.ip = ip;

} else {

  activity.result = "failure";
  activity.fault_description = "No IP address found";
}</source>

This script queries for any IP address attached to a network interface that points to the target CI in the incident. The script takes the first IP address that it finds and stores it in the workflow.scratchpad.ip variable that was defined in the Run Command activity. The Workflow script activity runs the script that returns the CI's IP address and stores it in the scratchpad variable. The Run Command activity gets the IP address of the target Linux server through the variable and executes the restart command on that computer.

RBA_Example_Run_Script2.png‎

Note	Note: This basic Workflow is functional, but lacks some useful details, such as Work Notes, which appear on the related incident and contain information about the attempts to restart the Linux server.
Refining the Workflow
Adding a server test and work notes that appear in the related incident can make our basic Workflow more usable.

Add the activity Orchestration > Test Server Alive before the Run Command activity and give it the following values:
Name: Is server alive
Port probes: ssh
Hostname: ${workflow.scratchpad.ip}
Click Submit.
If the target CI is alive, then the Workflow attempts to restart it.
Add the activity Tasks > Add Worknote after the Test Server Alive activity to manage the flow through the Failure exit.
Name: Server dead
Work Note: Orchestration: Server is dead, cannot restart.
Add the Add Worknote activity after the Run Command activity to exit the Workflow if the platform determines that the server was not shut down.
Name: Shutdown failure
Work Note: Orchestration: Server failed to shutdown. Cannot restart.
Click Submit.
The Workflow now resembles this:

RBA_Example_Workflow.png‎

To improve the usability of the Workflow further, add Test Server Alive activities to ensure that the server stops and restarts successfully, then add Worknote activities to communicate this to the incident.
