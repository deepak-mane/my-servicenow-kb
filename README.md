# my-servicenow-kb
My Servicenow Learnings
- [ServiceNow London Platform Admin](https://docs.servicenow.com/bundle/london-platform-administration/page/get-started/servicenow-overview/reference/r_AdministerServiceNow.html)
- [Search Knowledge Bases ServiceNow](https://hi.service-now.com/$knowledge.do)
- [Search ServiceNow SelfService](https://hi.service-now.com/nav_to.do?)
- [Playlists](https://www.youtube.com/user/servicenowdemo/playlists)
- [ServiceNow Developer Training](https://developer.servicenow.com/app.do#!/training/landing?v=london)
- [ServiceNow Developer Training](https://www.youtube.com/playlist?list=PLzTvAeLiW8AeO2Ep-qgufgOdLJ5UoA4hf)
- [Working with Dashboards](https://www.youtube.com/watch?v=ytI9JL4ifjU)
- [Advanced Dashboards](https://www.youtube.com/watch?v=Blik6EG9UGg)
- [System Configuration | Configuring Inbound Actions and Notifications](https://youtu.be/dhjLiwtT97E)
- [Inbound email actions](https://www.youtube.com/watch?v=C2FMo3l1swk)
- [ServiceNow Case Studies](http://www.fideltech.com/servicenow-case-studies/)
- [ServiceNow - How to Create SLAs](https://www.youtube.com/watch?v=1_T2VtFbldQ)
- [ServiceNow SLA | Introduction of SLA | What is SLA](https://www.youtube.com/watch?v=zMOoVokK3gI)


# Navigations for Admin
1. [Table Structure](https://portlandgeneraltest.service-now.com/table_columns.do)
2. To check Incident configurations -Type in Navigator incident.config
3. To check Problem configuratiions -Type in Navigatior problem.config
4. To check Incident table -Type in Navigator incident_list
5. To check Problem table -Type in Navigatior problem_list
6. To check attachments -Type in Navigator sys_attachment
7. To check Knowledge configuratiions -Type in Navigatior kb_knowledge.config
8. To check Subscrition details : [license_details_list.do](https://<instance-name>.service-now.com/license_details_list.do?sysparm_query=end_date%3E=javascript:gs.beginningOfToday()^start_date%3C=javascript:gs.endOfToday() )
9. Configuation Properties Applicaiton wise: 
    1. [Incident](Incident_Management_Properties.md)
    2. [Major Incident](Major_Incident_Management_Properties.md)
    3. Problem
    4. Request
    5. [Change](Change_Management_Properties.md)
    6. Knowledge
    7. Service Portal
    8. Service Level Mangeament
    9. Configuration Managment
    10. [Discovery](Discovery_Properties.md)  [Discovery Properties](https://<instance-name>.service-now.com/system_properties_ui.do?sysparm_category=Discovery&sysparm_title=Discovery%20Properties)
10. To check CI Class Manager [Open CI Class Manager](https://<instance-name>.service-now.com/$ciModel.do)
11. To check Plugins Activated https://<instance_name>.service-now.com/v_plugin_list.do
12. To [Export Data](Export_data_servicenow.md)  
13. Tale of Two Accounts for Admins[Duty Separation](https://snprotips.com/blog/2018/7/23/admin-duty-separation-with-a-single-account)
14. To Learn more about [filters](ServiceNow_Filters.md)

# Table Names
1. sys_filter_list.do - List of Saved Filters
2. incident_list.do - Incident Table
3. change_request_list.do - Change Table
4. problem_list.do - Problem Table

# ITSM Customer Lifecycle Plan: Valuable Resources for New and Existing Customers in IT Service Management
Whether you are a new customer or an existing customer, you want to realize value as quickly and effectively as possible with the ServiceNow platform.   Trying to manage your incidents or wanting to give your end users a simple and easy way to request services or trying to get a handle on your overall software and hardware inventory:   these are just a few things you may be focusing on.

This lifecycle guide is organized by the typical phases you'll go through as a customer of ServiceNow.   First, you'll plan, then implement, then use and adopt applications, and then upgrade and renew. Step through the lifecycle in order or pick and choose depending on where you are and what you need to accomplish. Come back often to see what additional information will bring you the most value.

Please take our survey so we can improve our content to meet your business needs.

| New Customer | Existing Customers | 
| --- |  --- | 
| Plan
ServiceNow Foundations Course
System Administration Training
Champion Enablement Get Started:   Program Management
Champion Enablement Go Live Communication and Training Guide
ITSM Process Guides
Implement ServiceNow
Implementation Bootcamp
For Express: Implementation Webinar
Implementation Best Practices
Enterprise Getting started videos
Applications on the ServiceNow Platform
Getting Started with Tables
User Interface | Overview
Getting Started with Forms
User Interface | Lists
User Interface | Application Navigator
Performing Basic Setup in Your Instance
Configuring Application Menus and Modules
ServiceNow Express Product Start Here videos
Customer Success Stories
Customer Success Best Practices
Guided SetUp |
Use additional ServiceNow applications
ITSM Value Realization Webinars:   Application Webinars
Application Communities (learn from your peers)
Asset Management
Change Management
Incident Management
Password Reset
Problem Management
Release Management
Adoption path (coming soon)
Learning Library
Product Documentation
Other Training and Resources
ITSM Measurement Framework   (webinar by Pink Elephant VP of R&D)
ServiceNow User Groups: SNUGs
Knowledge Conference
Upgrade and grow your use of ServiceNow
Adoption path (coming soon)
Family End-of-Life (EOL) Upgrade Guide
Prepare for an Upgrade
Upgrade Testing
Early Access
Learning Library
ServiceNow Development Path |




### if you dont understand wiki follow below steps. i am assuming that u dont already have transform map for that destination table. if u have then use that

- go to system import sets-->load data module
- enter table name..chose file(.xls file) make sure 1st row in excel match fields in your destination table.so it will automap.
- then click on create transform link
- give it a name,select destination table(table in which u want to upload data)
- click on auto map matching fields..if required fields do not match then click on mapping assist and match fields.
- set colesce true to any one field from related list. it will be your unique field
- click transform

### How to Earn Points [community.servicenow.com](https://community.servicenow.com/community?id=community_earning_points)
Your reputation in the community is based on the points and expertise you gain while performing different activities within the community.

- Earning Points
You earn points taking specific actions in the community. These points count towards your forum, topic or global level. The more points you earn, the higher you rank on the leaderboards.

- Badges - A badge is displayed on your profile as a trophy for completing a task in the community. See the list of badges you have unlocked and have yet to unlock on your profile.

- Points - Whenever you complete a task from the list below, you earn the corresponding number of points. See the list of tasks you have been awarded points for on your profile.

See the table below on what designated tasks earn points:

|Points	|Action |
| --- | --- |
|5	|Comment marked as helpful|
|10	|Answer marked as helpful|
|20	|Article bookmarked|
|20	|Blog marked as helpful|
|20	|Blog bookmarked|
|20	|Article marked as helpful|
|20	|Video bookmarked|
|30	|Video marked as helpful|
|40	|Answer marked correct for a question|


| Community Level | Points |
| --- | --- |
|Community Level 10  |100,000+ Points|
|Community Level 9  |50,000 Points|
|Community Level 8  |30,000 Points|
|Community Level 7  |15,000 Points|
|Community Level 6  |8,000 Points|
|Community Level 5  |4,000 Points|
|Community Level 4  |2,000 Points|
|Community Level 3  |1,000 Points|
|Community Level 2  |500 Points|
|Community Level 1  |200 Points|
