# BACKGROUND SCRIPT CODE VAULT
[Reference](https://www.servicenowelite.com/blog/2017/8/25/code-vault/background-scripts)
## RECORD QUERIES
### ACTIVE REQUESTS WITHOUT REQUESTED ITEMS
```
(function() {
var grRequest = new GlideRecord("sc_request");
grRequest.addEncodedQuery("active=true");
grRequest.query();
gs.print('Active Requests without Requested Items :(');
while (grRequest.next()) {
var gaRequestedItem = new GlideAggregate("sc_req_item");
gaRequestedItem.addQuery("request",grRequest.sys_id);
gaRequestedItem.addAggregate('COUNT');
gaRequestedItem.query();
var req = 0;
if (gaRequestedItem.next()) {
req = gaRequestedItem.getAggregate('COUNT');
if (req == 0) {
gs.print(grRequest.number);
}
}
}
})();
```

### DISTINCT OPERATING SYSTEMS OF CIS
```
(function() {
var gaServer = new GlideAggregate('cmdb_ci_server'); //GlideAggregate query
gaServer.addAggregate('count'); //Count aggregate (only necessary for a count of items of each OS)
gaServer.orderByAggregate('count'); //Count aggregate ordering
gaServer.groupBy('os'); //Group aggregate by the 'os' field
gaServer.query();
while(gaServer.next()){
var osCount = gaServer.getAggregate('count'); //Get the count of the OS group
//Print the OS name and count of items with that OS
gs.print('Distinct operating system: ' + gaServer.os + ': ' + osCount);
}
})();
RECORD BY SYSID
(function() {
var sysID = '965c9e5347c12200e0ef563dbb9a7156';//Replace with SysID
var grObject = new GlideRecord('sys_db_object');
grObject.addEncodedQuery('nameNOT LIKEts_^sys_update_nameISNOTEMPTY^nameISNOTEMPTY^name!=item_option_new_backup');
grObject.query();
while (grObject.next()) {
var tableName = grObject.getValue('name');
grTable = new GlideRecord(tableName);
grTable.addQuery('sys_id',sysID);
grTable.query();
if (grTable.next()) {
gs.print(gs.getProperty('glide.servlet.uri') + tableName + '.do?sys_id=' + sysID);
}
}
})();
ALL CI CLASSES
(function() {
var table = new TableUtils("cmdb_ci");
var ciTableList = j2js(table.getAllExtensions());
for (var i = 0; i < ciTableList.length; i++) {
gs.print(ciTableList[i]);
}
})();
FIND CI
(function() {
grCI = new GlideRecord('cmdb_ci');
grCI.addQuery('name','=','SAP WEB03');
grCI.query();
while (grCI.next()){
gs.print('CI Found: '+grCI.name);
}
})();
CI CLASSES USED
(function() {
var count = new GlideAggregate('cmdb_ci');
count.addAggregate('COUNT', 'sys_class_name');
count.query();
while (count.next()) {
var ciClass = count.sys_class_name;
var classCount = count.getAggregate('COUNT', 'sys_class_name');
gs.log("The are currently " + classCount + " configuration items with a class of " + ciClass);
}
})();
COMPUTERS WITHOUT SOFTWARE
//change the tablename if you want to query a different table like cmdb_ci_server
//add a parameter to the function call if you want to add a query
gs.print(getComputersWithoutSoftware('cmdb_ci_computer'));
function getComputersWithoutSoftware(compTableName, compQuery) {
var computers = [];
var grComputer = new GlideRecord(compTableName);
grComputer.addEncodedQuery(compQuery);
grComputer.query();
while (grComputer.next()) {
var gaInstalledSoftware = new GlideAggregate('cmdb_sam_sw_install');
gaInstalledSoftware.addQuery('installed_on', grComputer.sys_id);
gaInstalledSoftware.addAggregate('COUNT');
gaInstalledSoftware.query();
var comp = 0;
if (gaInstalledSoftware.next()) {
comp = gaInstalledSoftware.getAggregate('COUNT');
if (comp == 0) {
computers.push(grComputer.name.toString());
}
}
return computers;
}
DUPLICATE TASK NUMBERS
//Find Duplicate Task Numbers
gs.print(getDuplicates('task','number'));
function getDuplicates(tablename,val) {
var dupRecords = [];
var gaDupCheck = new GlideAggregate(tablename);
gaDupCheck.addQuery('active','true');
gaDupCheck.addAggregate('COUNT',val);
gaDupCheck.addNotNullQuery(val);
gaDupCheck.groupBy(val);
gaDupCheck.addHaving('COUNT', '>', 1);
gaDupCheck.query();
while (gaDupCheck.next()) {
dupRecords.push(gaDupCheck[val].toString());
}
return dupRecords;
}
DUPLICATE SERIAL NUMBERS
//Find Duplicate CIs by Serial Number
gs.print(getDuplicates('cmdb_ci_server','serial_number'));
function getDuplicates(tablename,val) {
var dupRecords = [];
var gaDupCheck = new GlideAggregate(tablename);
gaDupCheck.addQuery('active','true');
gaDupCheck.addAggregate('COUNT',val);
gaDupCheck.addNotNullQuery(val);
gaDupCheck.groupBy(val);
gaDupCheck.addHaving('COUNT', '>', 1);
gaDupCheck.query();
while (gaDupCheck.next()) {
dupRecords.push(gaDupCheck[val].toString());
}
return dupRecords;
}
GROUPS WITHOUT GROUP MEMBERS
findEmptyGroups();
function findEmptyGroups() {
var myGroups = [];
var grGroup = new GlideRecord("sys_user_group");
grGroup.addActiveQuery();
grGroup.query();
while (grGroup.next()) {
var gaGroupMember = new GlideAggregate("sys_user_grmember");
gaGroupMember.addQuery("group",grGroup.sys_id.toString());
gaGroupMember.addAggregate('COUNT');
gaGroupMember.query();
var gm = 0;
if (gaGroupMember.next()) {
gm = gaGroupMember.getAggregate('COUNT');
if (gm == 0) {
myGroups.push(grGroup.name.toString());
}
}
}
gs.print(myGroups);
}
FIND LOCATIONS WITH TASKS
(function() {
gs.print('Task Relationships: ');
var grLocation= new GlideRecord('cmn_location');
grLocation.query();
while (grLocation.next()) {
var count = new GlideAggregate('task');
count.addQuery('location',grLocation.sys_id);
count.addAggregate('COUNT');
count.query();
var tasks = 0;
if (count.next()) {
tasks = count.getAggregate('COUNT');
if (tasks > 0) {
gs.print('Location: '+grLocation.name+' | Location SysID: '+grLocation.sys_id+' | Task Count: '+tasks);
}
}
}
})();
FIND LOCATIONS WITH CIS
(function() {
gs.print('CI Relationships: ');
var grLocation= new GlideRecord('cmn_location');
grLocation.query();
while (grLocation.next()) {
var count = new GlideAggregate('cmdb');
count.addQuery('location',grLocation.sys_id);
count.addAggregate('COUNT');
count.query();
var cmdb = 0;
if (count.next()) {
cmdb = count.getAggregate('COUNT');
if (cmdb > 0) {
gs.print('Location: '+grLocation.name+' | Location SysID: '+grLocation.sys_id+' | CI Count: '+cmdb);
}
}
}
})();
TABLE ROW COUNTS
//Find row counts for each table in ServiceNow
(function() {
var grDictionary = new GlideRecord('sys_dictionary');
grDictionary.addQuery('internal_type', 'collection');
grDictionary.addQuery('name','!=','sys_template');
grDictionary.query();
while (grDictionary.next()) {
 var currentTable = grDictionary.name.toString();
 var count = new GlideAggregate(currentTable);
 count.addAggregate('COUNT');
 count.query();
 if (count.next()) {
 gs.log('Table Count: Table: '+currentTable+ ' contains '+ count.getAggregate('COUNT') + ' rows.');
 }
}
})();
FIND UNIQUE VALUES
findUnique('cmdb_ci_computer','os');//put the table and field you want to find unique
function findUnique(table,field) {
var au = new ArrayUtil();
var uniqueArray = [];
var grTable = new GlideRecord(table);
grTable.orderBy(field);
grTable.addNotNullQuery(field);
grTable.query();
while (grTable.next()) {
uniqueArray.push(grTable[field].toString());
}
gs.print('Unique Values: ' +au.unique(uniqueArray));
}

 
EXPORT TABLE INFORMATION
//Print Information about Fields in ServiceNow
(function() {
var grSection = new GlideRecord('sys_ui_section');
grSection.query();
while (grSection.next()) {
var grSectionElement = new GlideRecord('sys_ui_element');
grSectionElement.addQuery('sys_ui_section',grSection.sys_id);
grSectionElement.OrderBy('position');
grSectionElement.query();
while (grSectionElement.next()) {
var grLabel = new GlideRecord('sys_documentation');
grLabel.addQuery('table',grSection.name);
grLabel.addQuery('element',grSectionElement.element);
grLabel.query();
if (grLabel.next()) {
gs.print('View: '+grSection.view.title+', Table: '+grSection.name+', Field Label: '+grLabel.label+', Field: '+grLabel.name);
}
}
}
})();
FIND TEXT IN BUSINESS RULES
findit('incident');
function findit(str) { 
var scr = "";
var grScript = new GlideRecord('sys_script');
grScript.query();
while (grScript.next()) {
scr = grScript.script.toString();
if (scr.indexOf(str) > -1) {
gs.print(grScript.name);
}
}
}
FIND USERS WITHOUT PHOTOS
//Find Users without Photos
(function() {
var count = 0;
gs.print("Users Found without Photos:");
var grUser = new GlideRecord("sys_user");
grUser.addActiveQuery();
grUser.query();
while (grUser.next()) {
if (grUser.photo.getDisplayValue() == "") {
gs.print(grUser.user_name);
count++;
}
}
gs.print("Total:"+count);
})();
FIELD TRIP
//Finds all fields and how often they are used
(function() {
    //Calculate Field Counts
    var grDictionary = new GlideRecord('sys_dictionary');
    grDictionary.addQuery('internal_type','!=', 'collection');
    grDictionary.addQuery('name','!=','sys_template');
    grDictionary.addQuery('name','!=','fpv_floorplan');
    grDictionary.addQuery('name','!=','atf_input_variable');
    grDictionary.addQuery('name','!=','atf_output_variable');
    grDictionary.addQuery('name','DOES NOT CONTAIN','sys_upgrade_history_log');
    grDictionary.addQuery('name','DOES NOT CONTAIN','sys_metadata');
    grDictionary.addQuery('name','DOES NOT CONTAIN','ts_c_');
    grDictionary.addQuery('name','DOES NOT CONTAIN','ts_document');
    grDictionary.addQuery('name','DOES NOT CONTAIN','cmdb_metric');
    grDictionary.addQuery('name','DOES NOT CONTAIN','sys_ui');
    grDictionary.addQuery('name','DOES NOT CONTAIN','var__m');
    grDictionary.addQuery('name','DOES NOT CONTAIN','pa_dashboards');
    grDictionary.addQuery('name','!=','v_cluster_transaction');
    grDictionary.addQuery('name','!=','v_customer_uploads');
    grDictionary.addQuery('name','!=','v_cxs_search_resource');
    grDictionary.addQuery('name','!=','v_db_index');
    grDictionary.addQuery('name','!=','v_db_trigger');
    grDictionary.addQuery('name','!=','v_field_creator');
    grDictionary.addQuery('name','!=','v_field_editor');
    grDictionary.addQuery('name','!=','v_index_creator');
    grDictionary.addQuery('name','!=','v_logfiles');
    grDictionary.addQuery('name','!=','v_plugin');
    grDictionary.addQuery('name','!=','v_quota_transaction');
    grDictionary.addQuery('name','!=','v_scriptable_object');
    grDictionary.addQuery('name','!=','v_table_creator');
    grDictionary.addQuery('name','!=','v_table_editor');
    grDictionary.addQuery('name','!=','v_transaction');
    grDictionary.addQuery('name','!=','v_user_session');
    grDictionary.addQuery('name','!=','v_wf_validation_report');
    grDictionary.addQuery('name','!=','v_ws_creator');
    grDictionary.addQuery('name','!=','v_ws_editor');
    grDictionary.addQuery('name','!=','v_ws_field_creator');
    grDictionary.addQuery('name','!=','v_ws_field_editor');
    //grDictionary.orderBy('name');
    grDictionary.query();
    while (grDictionary.next()) {
        var currentTable = grDictionary.name.toString();
        var count = new GlideAggregate(currentTable);
        count.addQuery(grDictionary.element, '!=', '');
        count.addAggregate('COUNT');
        count.query();
        if (count.next()) {
            gs.log(grDictionary.name + ', ' + grDictionary.sys_id + ' = ' + count.getAggregate('COUNT'));
        }
    }
})();
FIND OLDEST RECORD
(function() {
  var titleMessage = "Table name | Sys Id | Created | Created By";
  gs.log(titleMessage);
  //Create DB Object Array
  var dbObjectArray = [];
  var grDBObj = new GlideRecord('sys_db_object');
  grDBObj.addEncodedQuery('nameNOT LIKEitem_option_new_backup');
  grDBObj.addEncodedQuery('nameNOT LIKEts_c_');
  grDBObj.addEncodedQuery('nameNOT LIKEv_');
  grDBObj.addEncodedQuery('nameNOT LIKEsh$');
  grDBObj.addEncodedQuery('nameNOT LIKEnp$');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_template');
  grDBObj.addEncodedQuery('nameNOT LIKEsyslog');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_email');
  grDBObj.addEncodedQuery('nameNOT LIKEindex');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_history');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_translated');
  grDBObj.addEncodedQuery('nameNOT LIKEsysevent');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_metadata');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_schema');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_attachment');
  grDBObj.addEncodedQuery('nameNOT LIKEsys_amb_message');
  grDBObj.addEncodedQuery('nameNOT LIKEts_word');
  grDBObj.addEncodedQuery('nameNOT LIKEts_phrase');
  grDBObj.addEncodedQuery('nameNOT LIKEts_document');
  grDBObj.addEncodedQuery('nameNOT LIKEecc_queue');
  grDBObj.addEncodedQuery('nameNOT LIKEwf_log');
  grDBObj.query();
	while (grDBObj.next()) {
		dbObjectArray.push(grDBObj.name.toString());
	}
  //gs.log(dbObjectArray);
  //Gather Table Information
  for (var i = 0; i < dbObjectArray.length; i++) {
    var grTable = new GlideRecord(dbObjectArray[i]);
    grTable.addQuery('sys_created_on','!=','');
    grTable.orderBy('sys_created_on');
    grTable.setLimit(1);
    grTable.query();
    if (grTable.next()){
      var message = dbObjectArray[i] + " | ";
      message += grTable.sys_id + " | ";
      message += grTable.sys_created_on + " | ";
      message += grTable.sys_created_by;
      gs.log(message);
    }
  }
})();
GLIDE SCHEDULE QUERIES
(function() {
	var grSchedule = new GlideRecord('cmn_schedule');
	
	grSchedule.addQuery('name','6-6 weekdays excluding holidays');
	grSchedule.query();
	gs.print("grSchedule query: " + grSchedule.getEncodedQuery() + " = " + grSchedule.getRowCount());
	if (grSchedule.next()){
		//var startDate = new GlideDateTime('2017-09-26 9:00:00');
		//var endDate = new GlideDateTime('2017-09-26 11:30:00');
		var startDate = new GlideDateTime();
		startDate.setDisplayValue("2017-09-26 9:00:00");
		var endDate = new GlideDateTime();
		endDate.setDisplayValue("2017-09-26 11:30:00");
		gs.print("startDate: " + startDate);
                gs.print("endDate: " + endDate);
		// Creates a schedule with 6-6 weekdays (US/Central)
		var schedule = new GlideSchedule(grSchedule.sys_id);
		schedule.setTimeZone('US/Central');
		//var schedule = new GlideSchedule();
		//schedule.load(grSchedule.sys_id);

		gs.print("schedule name: " + schedule.getName());
		var duration = schedule.duration(startDate, endDate);
		gs.print("Duration Difference "+duration.getDurationValue());
		gs.print("Numeric Difference "+duration.getNumericValue());
	}
})();
RECORD UPDATES
Be careful!!! Always test Background Scripts first in a development instance.

ADD PREFIX OR SUFFIX
//Replace the function parameters below call with your own needs
addPrefixSuffixToField('prefix','incident','active=true^caller_id=681ccaf9c0a8016234234400b98a06818d57c7','short_description','Urgent: ');

function addPrefixSuffixToField(prefixOrSuffix, myTableName, myQuery, myFieldName, valueToAdd) {
var gr = new GlideRecord(myTableName);
gr.addEncodedQuery(myQuery)
gr.query();
var updateCount = 0;
while (gr.next()) {
if (prefixOrSuffix == 'prefix') {
gr[myFieldName] =valueToAdd+gr[myFieldName];
}
if (prefixOrSuffix == 'suffix') {
gr[myFieldName] = gr[myFieldName]+valueToAdd;
}
gr.setWorkflow(false);
gr.autoSysFields(false);
//gr.update();
updateCount++;
}
gs.print('Records Updated: '+ updateCount);
}
DELETE COMPUTERS
(function() {
var grComputer = new GlideRecord("cmdb_ci_computer");
grComputer.addEncodedQuery('sys_created_by=mikekaufman')
grComputer.query();
gs.log('grComputer Query: ' + grComputer.getEncodedQuery() + ' = ' + grComputer.getRowCount());
var deleteCount = 0;
while(grComputer.next()){
grComputer.setWorkflow(false);
//grComputer.deleteRecord();
deleteCount++;
}
gs.print('Records Deleted: '+ deleteCount);
})();
DELETE MODELS
(function() {
var grModel = new GlideRecord("cmdb_model");
grModel.addEncodedQuery('sys_created_by=mikekaufman');
grModel.query();
gs.log('grModel Query: ' + grModel.getEncodedQuery() + ' = ' + grModel.getRowCount());
while (grModel.next()) {
//grModel.deleteRecord();
}
})();
DELETE DUPLICATE ATTACHMENTS
(function() {
var grAttachment = new GlideRecord('sys_attachment');
grAttachment.addQuery('table_name', 'LIKE', 'ZZ_YY%');
grAttachment.orderBy('table_sys_id');
grAttachment.orderByDesc('sys_created_on');
grAttachment.query();
var lastID = 'not_a_match';
var lastFile = 'not_a_match';
while (grAttachment.next()) {
var isDuplicate = (lastID == grAttachment.table_sys_id) && (lastFile == grAttachment.file_name);
lastID = grAttachment.table_sys_id;
lastFile = grAttachment.file_name;
gs.print(grAttachment.table_sys_id + ' ' + grAttachment.table_name + ' ' + grAttachment.file_name + ' ' + grAttachment.sys_created_on + ' ' + isDuplicate);
if (isDuplicate)
//grAttachment.deleteRecord();
}
})();

 
DELETE OOB TABLE DATA
//Only use if you mean it, will delete all table data
//CMDB
deleteTableData("cmdb_ci");
deleteTableData("cmdb_sam_sw_install");
deleteTableData("cmdb_model");
deleteTableData("alm_asset");
deleteTableData("alm_hardware");
//ITSM
deleteTableData("incident");
deleteTableData("change_request");
deleteTableData("cert_follow_on_task");
deleteTableData("problem");
deleteTableData("sc_request");
deleteTableData("sc_req_item");
deleteTableData("sc_task");
//Approvers
deleteTableData("sysapproval_group");
deleteTableData("sysapproval_approver");
//PPS
deleteTableData("pm_project");
deleteTableData("pm_project_task");
deleteTableData("resource_plan");
deleteTableData("planned_task_baseline");
deleteTableData("planned_task_baseline_item");
deleteTableData("pm_m2m_portfolio_project");
deleteTableData("pm_portfolio_group_resource");
deleteTableData("pm_portfolio_issue");
deleteTableData("pm_portfolio_project");
deleteTableData("pm_portfolio_user_resource");

function deleteTableData(table) {
var gr = new GlideRecord(table);
gr.query();
//gr.deleteMultiple();
}
DELETE SOFTWARE WITHOUT COMPUTER
(function() {
var gr = new GlideRecord("cmdb_sam_sw_install");
gr.addEncodedQuery('installed_on=NULL')
gr.query();
gs.log('gr Query: ' + gr.getEncodedQuery() + ' = ' + gr.getRowCount());
var deleteCount = 0;
while(gr.next()){
gr.setWorkflow(false);
//gr.deleteRecord();
deleteCount++;
}
gs.print('Records Deleted: '+ deleteCount);
})();
MASS CLOSE CHANGES
//Mass Close Changes after a certain date
(function() {
var grChange = new GlideRecord('change_request');
grChange.addQuery('opened_at','<=','2011-05-17 11:28:26');
grChange.query();
gs.log('grChange Query: ' + grChange.getEncodedQuery() + ' = ' + grChange.getRowCount());
while (grChange.next()){
grChange.state = '3';
grChange.active = 'false';
grChange.setWorkflow(false);
//grChange.update();
gs.log('Closed Change: ' + grChange.number);
}
})();
MASS CLOSE INCIDENTS
(function() {
var grIncident = new GlideRecord('incident');
grIncident.addQuery('opened_at','<=','2011-05-17 11:28:26');
grIncident.query();
gs.log('grIncident Query: ' + grIncident.getEncodedQuery() + ' = ' + grIncident.getRowCount());
while (grIncident.next()){
grIncident.state = '7';
grIncident.incident_state = '7';
grIncident.active = 'false';
grIncident.close_code = 'Completed';
grIncident.close_notes = 'Cloned Incident Closed';
grIncident.setWorkflow(false);
//grIncident.update();
gs.log('Closed Incident: ' + grIncident.number);
}
})();
REMOVE COMMAS FROM STRING FIELD
//Replace 'table name here','query here if needed','field name here' ith your parameters for the comma remove
removeCommas('table name here','query here if needed','field name here');
function removeCommas(rcTableName,rcEncodedQuery,rcFieldName) {
 var grCommaRemove = new GlideRecord(rcTableName);
 grCommaRemove.addEncodedQuery(rcEncodedQuery)
 grCommaRemove.query();
 var updateCount = 0;
 while(grCommaRemove.next()){
 grCommaRemove[rcFieldName] = grCommaRemove[rcFieldName].replace(/,/g , "");
 //grCommaRemove.update();
 updateCount++;
 }
 gs.print('Records Updated: '+ updateCount);
}
REPLACE SEMICOLON WITH A COMMA
//Replace 'table name here','query here if needed','field name here' with your parameters

replaceSemiColons('table name here','query here if needed','field name here');
function replaceSemiColons(rcTableName,rcEncodedQuery,rcFieldName) {
 var updateCount = 0;
 var grSCR = new GlideRecord(rcTableName);
 grSCR.addEncodedQuery(rcEncodedQuery)
 grSCR.query();
 while(grSCR.next()){
 grSCR[rcFieldName] = grSCR[rcFieldName].replace(/;/g , ",");
 //grSCR.update();
 }
RESET KB VIEW COUNTERS
(function() {
var grKB = new GlideRecord("kb_knowledge");
grKB.addEncodedQuery('kb_knowledge_base=2d9212c04f35fa00a064d49f0310c714');
grKB.query();
gs.log('grKB Query: ' + grKB.getEncodedQuery() + ' = ' + grKB.getRowCount());
while (grKB.next()) {
grKB.sys_view_count=0;
//grKB.update();
}
})();
SYNC ASSET RECORDS
(function() {
 var grCI = new GlideRecord("cmdb_ci_computer");
 grCI.query();
var updateCount = 0;
 while(grCI.next()){
 //gs.print('Syncing '+grCI.serial_number);
 var ca = new AssetAndCISynchronizer();
 ca.syncRecords(grCI, 'alm_asset');
 updateCount++;
 }
}
gs.print('Records Updated: '+ updateCount);
})();
LOCKOUT USERS
(function() {
var grUser = new GlideRecord("sys_user");
grUser.addEncodedQuery('active=true^roles!=admin');
grUser.query();
gs.print("User query: " + grUser.getEncodedQuery() + " = " + grUser.getRowCount());
while (grUser.next()) {
grUser.locked_out = true;
//Uncomment out the bottom line when you are ready to run this!
//grUser.update();
gs.print(grUser.getDisplayValue() + " was disabled");
}
})();
SET PASSWORD
//Resets password for every single user, overwriting their existant password. Use with caution. Replace abc123 with the string in question.
(function() {
var grUser= new GlideRecord("sys_user");
grUser.query();
gs.print("User query: " + grUser.getEncodedQuery() + " = " + grUser.getRowCount());
while(grUser.next()){
grUser.user_password.setDisplayValue("abc123");
gs.log("updating password for " + grUser.user_name);
//grUser.update();
}
})();
ADD OUTAGE NUMBERS
(function() {
var grOutage = new GlidegrOutageord('cmdb_ci_outage');
grOutage.addQuery('u_number','');
grOutage.query();
gs.print("grOutage query: " + grOutage.getEncodedQuery() + " = " + grOutage.getRowCount());
while(grOutage.next()){
 grOutage.u_number =new NumberManager(grOutage.sys_meta.name).getNextObjNumberPadded();
 grOutage.setWorkflow(false); //Do not run business rules
 grOutage.autoSysFields(false); //Do not update system fields
 grOutage.update();
}
})();
```
