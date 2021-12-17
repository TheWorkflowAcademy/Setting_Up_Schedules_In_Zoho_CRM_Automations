# Setting_Up_Schedules_In_Zoho_CRM_Automations


## Use Case
There may be times wherea function or action needs to run in Zoho CRM at set intervals, such as updating Current Age field for all Contacts on a weekly basis. Setting up a schedule in automation allows you this capability without having to manually edit a record each time you want a function to trigger. If you are needing to update more than 200 records at a time, check out the Workflow Academy's *[API pagination Github repo](https://github.com/TheWorkflowAcademy/api-pagination-zohocrm)*.





## Set Up

To set up a schdedule, navigate to Settings > Automation > Schedules. Click on "Create New Schedule".

<img src="create.PNG" width="600">

Select either "Writing Function" or "From existing functions". Note - if you decide to use a previously written function, use a parameterless function (eg: don't select a module and id) since these actions aren't tied to a specific record. For new functions, you won't see the usual list of modules if you try to add parameters. Don't select any modules. 
For this tutorial, we will be writing a new function to update the Current Age field.

## Write Your Function

There are a couple of ways to implement this. If you don't anticipate having more than 1000 records at any time to search, your function may look like the sample below.
First, you will need to get a list of all records in the module, or custom view, depending on your use case. Next, iterate over all records that you want to perform your function on. This particular function calculates the age based on the Contact Date of Birth field, then sets the Current Age field accordingly.

```
getContacts = zoho.crm.getRecords("Contacts");
for each r in getContacts
{
	contactID = r.get("id");
	dob = r.get("Date_of_Birth");
	if(dob != null){
		daysBetween = dob.daysBetween(zoho.currentdate);
		calAge = (daysBetween / 365).floor();
	}
	updateRecord = zoho.crm.updateRecord("Contacts",contactID,{"Current_Age":calAge});
}
```
OR

If there are more than 1000 records that will need to be updated at any one time, add your pagination code first. If you need help setting this up, please see WFA's repo *[here](https://github.com/TheWorkflowAcademy/api-pagination-zohocrm)*. 

```
allRecords = List();
pageIterationList = {1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25};
iterationComplete = false;
crmModule = "Contacts";
perPage = 200;
for each  page in pageIterationList
{
	if(iterationComplete == false)
	{
		response = invokeurl
		[
			url :"https://www.zohoapis.com/crm/v2/" + crmModule + "?page=" + page + "&per_page=" + perPage
			type :GET
			connection:"crm"
		];
		records = response.get("data");
		//info records;
		allRecords.addAll(records);
		info allRecords;
		if(records.size() < perPage)
		{
			iterationComplete = true;
		}
	}
}

```
Next, use the allRecords list to iterate through and update each record.


```
getContacts = allRecords;
for each r in getContacts
{
	contactID = r.get("id");
	dob = r.get("Date_of_Birth");
	if(dob != null){
		daysBetween = dob.daysBetween(zoho.currentdate);
		calAge = (daysBetween / 365).floor();
	}
	updateRecord = zoho.crm.updateRecord("Contacts",contactID,{"Current_Age":calAge});
}
``


* A Zoho Creator form with:
  * a note field
  * an Account ID field
* User input workflow to initalize the table

You will need to have in place:

* CRM oauth connection in Creator


<img src="schedule.PNG">

```

add code block here

```
