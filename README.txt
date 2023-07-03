Thank you for downloading this Demo Automation Template for UiPath Communications Mining! Below are some instructions to help you get started. 
We hope this template helps give you a quickstart in how you can begin leveraging UiPaths Communications Mining capability in your automations!

***Please Note, this is a demo template and not intended to be ready to go for Production. Please follow proper development practices when building for production. See UiPath Academy for more.***


What you need:
1. This Template!
2. Access to a UiPath Automation Cloud
3. Access to UiPath Communications Mining instance (please check with your account team to find out how you can get access if you do not already have it).
4. A UiPath Communications Mining instance trained on your dataset. Instructions on how to do this can be found below:
		- Getting Started: https://support.reinfer.io/support/solutions/folders/48000590868
		- Model Training & Maintenance (Uploading a CSV file Data Source): https://support.reinfer.io/support/solutions/articles/48001161525-uploading-a-csv-file-into-a-source  
5. An ITSM Environment of your choice.
6. UiPath Studio to configure the template and build your automation.


Overview of Relevant Project Files:
WORKFLOWS:
 - ITSM_Main.xaml: Main Workflow that runs the automation flow. During execution, it uses additional xaml files to execute various aspects of the process.
 - Get_TicketData.xaml: Workflow to grab your ITSM tickets. You will need to configure it to your ITSM environment through API or UI extraction methods (default is API).
 - GetOne_Ticket.xaml: Workflow to iterate through a data table of the ITSM ticket data, one at a time, to process each ticket.
 - Get Email.xaml: This file is not used, but! You can replace the Get_TicketData.xaml with this one to configure it for reading emails! Give this one a try once you have the ITSM flow working!
 - Framework > ReadConfigFile.xaml: used to read in the Config.xlsx values (see below).
 
 - Config.xlsx: Add in your Communications Mining Token and Request URL for making the API call to UiPath Communications Mining.
 
 - json_templates:
 	- predict.json: proper format for the Comms Mining API Call Body.
	- servNow.json: proper format for the Service Now Table API as used in the Dev Dives session. Left this in to provide guidance/an example.

 
General Instructions:

1. From the "Start" of the flow, walk through each workflow/activity. Each location where you need to either do some setup or configuration will be Commented and/or Annotated into the activities.

2. The first activity you will need to do is update the "Get_TicketData.xaml" Invoked workflow, right after the "INIT" step, with an API Call or Ui Automation to extract your ticket data from your ITSM system.
	The output must be in DataTable format with at least the following fields: Unique ID, Ticket Submitter, Subject/Short Description, Detailed Description. Assign that DataTable to out_TicketRecords.
	
3. That datatable is fed into "GetOne_Ticket.xaml". The workflow maps a tickets data from the datatable to variables, as outlined below. Adjust the assign activities to pull from your column headers.
	[ITSM Data Field = UiPath Workflow Variable]
	Unique ID = out_TicketID
	Ticket Submitter = out_TicketSender
	Subject/Short Description = out_TicketSubject
	Detailed Body/Description = out_TicketDesc
	
4. The "Process Ticket" step should work as long as you have correctly setup the Config.xlsx file and configured the "GetOne_Ticket.xaml" activity.

5. In the "Action Based on AI Result" Activity, update the classification categories and switch activity cases to match the labels in your Communications Mining Instance.
	Ensure the names of the Cases match the classification labels you have in Communications Mining
	Update the Expression Field in the Switch Activity by updating the labels to match your Cases as well.
	
6. For each Case in the switch activity, update the action you would like the automation to take based on a ticket getting that classification. 
	In the template, each case has a log acivity to log the ticket's classification.
	
7. Now run your automation! You will see there is an Option path for Human Validation. In the template this does nothing, but you can configure the flow to send items to Action Center for HITL.