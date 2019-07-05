# ServiceNow Inbound Email Actions

## Inbound email actions enable you to define the actions an instance takes when receiving email.

Inbound email actions are similar to business rules: both use conditions and scripts that take action on a target table. An inbound email action checks the email for a watermark that associates it with a task and checks for other conditions. If the conditions are met, the system takes the inbound email action that you configure. The system can take two types of actions:
Record action: setting a value for a field in the target table.
Email reply: sending an email back to the source that triggered the action.
By default, if an email has no identifiable watermark, an inbound email action attempts to create an incident from the message. If the email has a watermark of an existing incident, an inbound email action updates the existing incident according to the action's script.

## Inbound email action types
![alt text](./images/inbound-action-type.png)


|Order|	Type	| Criteria|
|---|---|---|
|1	|Forward | 	*<ol><li>The system classifies an email as a forward only when it meets all these criteria:</li><li>The subject line contains a recognized forward prefix such as FW:.</li><li>The email body contains a recognized forward string such as From:.</li><li>The system classifies any email that meets these criteria as a forward, even if the message contains a watermark or record number that otherwise classifies it as a reply.</li></ol>* |
|2	|Reply	|*<ol><li>The system classifies an email as a reply when it fails to match it to the forward inbound action type and it meets any one of these criteria:</li><li>The subject line or email body contains a recognized watermark such as Ref:MSG0000008.</li><li>There is no watermark and the Reply-To header contains a recognized record number such as INC0005574.</li><li>There is no watermark and the subject line contains a recognized reply prefix such as RE: and a recognized record number such as INC0005574</li></ol>* |
|3	|New	|*<ol><li>The system classifies an email as new when it fails to match it to the forward and reply inbound action types.</li></ol>* |


### Incident

1.) Creating Incident : This inbound email action is triggered when an email is sent to ServiceNow and the email is not a reply or forward. This inbound email action can set the following fields on a new Incident:

  - assigned_to
  - priority

    In addition to being able to explicitly set the values of the above fields within the email, 
    the following is done automatically:

    1. The Incident caller_id is set to the the user who sent the email.
    2. The email subject is set as the Incident short description.
    3. The whole email is added to the Incident as a comment.
    4. The Incident category is set to "inquiry".
    5. The Incident state is set to "1".
    6. The Incident notify is set to "2".
    7. The Incident contact type is set to "email".

```
Example email: This email will create a new Incident with the following:

1. The Incident caller is set to "Fred Luddy".
2. The Incident short description will be set to "Not able to connect to wireless network"
3. The whole email body is added to the Incident as a comment.
4. The Incident is assigned to "Bow Ruggeri" if the sender has the itil role.
5. The Incident category is set to "inquiry".
6. The Incident state is set to "1".
7. The Incident notify is set to "2".
8. The Incident contact type is set to "email".
9. The Priority is set to "2" if the sender has the itil role.

-----

From: 	Fred Luddy <fred.luddy@example.com>
Subject: 	Not able to connect to wireless network
Date: 	June 11, 2013 1:44:55 PM PDT
To: 	        ServiceNow

The wireless network has been down for 30 minutes now. 

assign: Bow Ruggeri

-----

```
2.) Updating Incidents : This inbound email action can update the following fields on an Incident:
- assigned_to
- priority
- category
- short_description

```
Example reply email: this reply will update comments for the Incident with "Our engineers are on this - should see resolution in a couple hours.", assign the Incident to David Loo, and set priority to "2".

-----

From: 	Fred Luddy <fred.luddy@example.com>
Subject: 	Re: Incident INC0010008 has been assigned to you
Date: 	June 10, 2013 10:47:00 AM PDT
To: 	        ServiceNow

Our engineers are on this - should see resolution in a couple hours.

priority: 2
assigned_to: david.loo
```


