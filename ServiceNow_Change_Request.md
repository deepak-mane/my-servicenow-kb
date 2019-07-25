# Change Management

The ServiceNow Change Management application provides a systematic approach to control the life cycle of all changes, facilitating beneficial changes to be made with minimum disruption to IT services.

ServiceNow Change Management integrates with the Vulnerability response plugin to introduce extra functionality within Change Management.

|Explore|Set up|Administer|Use|
|---|---|---|---|
|Change types|Activate Change Management plugins|Configure ability to copy a change request|Create a change request|
|State model and transitions|Change Management properties|Configure standard change catalog properties|Associated CIs on a change request|
|Standard change catalog|Configure Change Management|Create blackout and maintenance schedules|Process a change request|
|Domain separation in Change Management||Add a new change request type|Analyze change request risk and impact|
|||Risk assessment|Change Advisory Board (CAB) workbench|
|||Out-of-the-box Change Management Performance Analytics Solutions||


|	Table	|	Element	|	Value	|	Dependent value	|	Label	|	Sequence	|
|	----	|	----	|	----	|	----	|	----	|	----	|
|	change_request	|	state	|	'-5	|		|	New	|	1	|
|	change_request	|	state	|	'-4	|		|	Assess	|	2	|
|	change_request	|	state	|	'-3	|		|	Authorize	|	3	|
|	change_request	|	state	|	'-2	|		|	Scheduled	|	4	|
|	change_request	|	state	|	'-1	|		|	Implement	|	5	|
|	change_request	|	state	|	0	|		|	Review	|	6	|
|	change_request	|	state	|	3	|		|	Closed	|	7	|
|	change_request	|	state	|	4	|		|	Canceled	|	8	|



|	Table	|	Element	|	Value	|	Dependent value	|	Label	|	Sequence	|
|	----	|	----	|	----	|	----	|	----	|	----	|
|	change_request	|	phase_state	|	open	|	requested	|	Open	|	1	|
|	change_request	|	phase_state	|	open	|	accept	|	Open	|	1	|
|	change_request	|	phase_state	|	open	|	build	|	Open	|	1	|
|	change_request	|	phase_state	|	open	|	plan	|	Open	|	1	|
|	change_request	|	phase_state	|	work in progress	|	requested	|	Work in Progress	|	2	|
|	change_request	|	phase_state	|	work in progress	|	accept	|	Work in Progress	|	2	|
|	change_request	|	phase_state	|	work in progress	|	build	|	Work in Progress	|	2	|
|	change_request	|	phase_state	|	work in progress	|	plan	|	Work in Progress	|	2	|
|	change_request	|	phase_state	|	approved	|	plan	|	Approved	|	3	|
|	change_request	|	phase_state	|	approved	|	build	|	Approved	|	3	|
|	change_request	|	phase_state	|	approved	|	requested	|	Approved	|	3	|
|	change_request	|	phase_state	|	approved	|	accept	|	Approved	|	3	|
|	change_request	|	phase_state	|	rejected	|	plan	|	Rejected	|	4	|
|	change_request	|	phase_state	|	rejected	|	build	|	Rejected	|	4	|
|	change_request	|	phase_state	|	rejected	|	requested	|	Rejected	|	4	|
|	change_request	|	phase_state	|	rejected	|	accept	|	Rejected	|	4	|
|	change_request	|	phase_state	|	testing	|	accept	|	Testing	|	5	|
|	change_request	|	phase_state	|	testing	|	build	|	Testing	|	5	|
|	change_request	|	phase_state	|	implementation	|	build	|	Implementation	|	6	|
|	change_request	|	phase_state	|	on hold	|	requested	|	On Hold	|	7	|
|	change_request	|	phase_state	|	on hold	|	build	|	On Hold	|	7	|
|	change_request	|	phase_state	|	on hold	|	accept	|	On Hold	|	7	|
|	change_request	|	phase_state	|	on hold	|	plan	|	On Hold	|	7	|
|	change_request	|	phase_state	|	complete	|	requested	|	Complete	|	8	|
|	change_request	|	phase_state	|	complete	|	build	|	Complete	|	8	|
|	change_request	|	phase_state	|	complete	|	accept	|	Complete	|	8	|
|	change_request	|	phase_state	|	complete	|	plan	|	Complete	|	8	|
