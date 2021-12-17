# Setting_Up_Schedules_In_Zoho_CRM_Automations


## Use Case
There may be times where we need a function or action to run in Zoho CRM repeatedly at set intervals, such as updating the age or an age group for all Contacts on a weekly basis. Setting up a schedule in automation allows you this capability without having to manually edit a record to trigger a function. If you are needed to update more than 200 records at a time, check out the Workflow Academy's *[API pagination Github repo](https://github.com/TheWorkflowAcademy/api-pagination-zohocrm)*.

<img src="schedule.PNG">


## Set Up

To set up a schdedule, navigate to Settings > Automation > Schedules. Click on "Create New Schedule".

<img src="create.PNG" width="600">

Select either "Writing Function" or "From existing functions". Note - if you decide to use a previously written function, use a parameterless function (eg: don't select a module and id) since these actions aren't tied to a specific record. For new functions, you won't see the usual list of modules if you try to add parameters. Don't select any modules. 
For this use case



* A Zoho Creator form with:
  * a note field
  * an Account ID field
* User input workflow to initalize the table

You will need to have in place:

* CRM oauth connection in Creator




```

add code block here

```
