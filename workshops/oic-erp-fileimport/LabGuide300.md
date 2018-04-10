# Lab 300 - Create Integration Flow

Updated: 03-09-18

## Introduction

This is the third of several labs that are part of the **ICS ERP Development Workshop**.

In this lab, you will learn how to create a basic ICS Integration using the connections that you created in the previous lab.

**To log issues**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives

- Create your first Integration using the ERP and FTP connections that were previously created in lab 200, before testing them in Lab 400.

## Required Artifacts

- The following lab and an Oracle Public Cloud account that will be supplied by your instructor.

### **STEP 1** Log in

- Login to the ICS Service Console

- If you are not already logged in: From your browser (Firefox or Chrome recommended) login to the ICS Console.

- Enter your `User Name` and `Password` and click **Sign In** same way as done in Lab 100.

 **NOTE:** the **User Name and Password** values will be given to you by your instructor.
 
 - Once you enter, it should look like below screenshot.
 
 	![](images/100/image003.png)

 - You are presented with the home page and overlay for the ICS Service Console - which we already went through ICS in Lab 100

- Click on the Integration tab on left hand side menu. It will open the Integration page that has all the integrations. 

	![](images/100/image004e.png)
	![](images/100/image004f.png) 

	Now we are ready to check the connections.
  
### **STEP 2**: Check your Connections

- From the Integration Cloud Dashboard, click on the "Connections".

- ICS console will be loaded in new window.

- If you see anything other than green checks on the right side of your connections, then go back to the previous steps in Lab 200 and make sure your connections are configured correctly.

	![](images/300/image102.png)

- Now go back to the "Integrations".

### **STEP 3** ICS Development

- Creating Integration 

- In the top right of the Integrations page, click “Create”.

	![](images/300/image001.png)

- Select the “Orchestration” style/pattern.

	![](images/300/image002.png)

- Choose "Schedule" for triggering the integration. Enter the integration name “ICSERP  File Import_XX”, replacing "XX" with your User Number. Then, click “Create”.

	![](images/300/image003.png)

## Adding First FTP Connection 

- Now, we will edit the orchestration for this integration. From the left hand panel, by expanding "Invokes" and then "FTP" in the right-hand side palette. Drag the component to the orchestration flow digram, as follows:

	![](images/300/image323.png)

- The Wizard for configuring the FTP endpoint will appear. On the Basic Info page, enter the name as "DownloadFBDZipFileFromFTP", as shown below. Then,  click "Next" at the top.

	![](images/300/image007.png)

- Next, on the Operations page, Select operation as "Download File" and transfer mode as "Binary". Provide the input directory and filename as shown below in the screenshot. Input directory is where you have placed your file in FTP and filename is the name of the file. Enter the download directory in ICS as shown below. Don't select any other fields. Then, click "Next".

	![](images/300/image008.png)

- A summary of the new endpoint is presented. Review it and click "Done".

	![](images/300/image010.png)

- The orchestration flow should now look like this:

	![](images/300/image011.png)

- The icons in the diagram can be stretched to add space, as follows:

	![](images/300/image012.png)

- The next step is to delete the mapping for FTP adapter. So right click on the mapping "DownloadFBDZipFileFromFTP" and click on the hamburger menu. Click on the delete. It asks for confirmation and click on "yes" to confirm. This deletes the mapping.

	![](images/300/image012a.png)
	![](images/300/image012b.png)
	![](images/300/image012c.png)

- The next step is to unzip the file for staging. From the right hand panel, by expanding "Actions" and locate Stage file. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image013.png)
	![](images/300/image013a.png)

- You are prompted to name the action. Call it "UnzipStagedFiles". click "Next".

	![](images/300/image014.png)

- Next, choose stage file operation as "unzip file". Next, click on the pencil button next to box. This opens a new pop-up provide the details. Provide the details as shown in the below screenshot under "expression". Click on "save" and hit "exit Expression Builder" to go back to previous screen. Repeat the step for all the boxes and provide the details as highlighted in the screenshot. Click on "Next" once everything is filled out.

	![](images/300/image015d.png)
	![](images/300/image015a.png)
	![](images/300/image015b.png)
	![](images/300/image015.png)

- Check the details are right in the summary section and click "Done".

	![](images/300/image016.png)

- The orchestration flow should now look like this:

	![](images/300/image017.png)

- The next step is to list the unzipped files. From the right hand panel, by expanding "Actions" and locate Stage file. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image018.png)
	![](images/300/image018a.png)

- You are prompted to name the action. Call it "ListStageUnzippedFiles". click "Next".

	![](images/300/image019.png)

- Next, choose stage file operation as "List file". Next, click on the pencil button next to box. This opens a new pop-up provide the details. Provide the details as shown in the below screenshot under "expression". Click on "save" and hit "exit Expression Builder" to go back to previous screen. For specify the file pattern to use .csv. Click "List files Recursively". "Next" once everything is filled out.

	![](images/300/image020a.png)
	![](images/300/image020b.png)
	![](images/300/image020c.png)
	![](images/300/image020d.png)
	![](images/300/image020e.png)

- Check the details are right in the summary section and click "Done".

	![](images/300/image020f.png)

- The orchestration flow should now look like this:

	![](images/300/image020g.png)

- The next step is to loop through the unzipped files. From the right hand panel, by expanding "Actions" and locate "For Each" under Repeat panel. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image021.png)
	![](images/300/image021a.png)

- You are prompted to name the action. Call it "LoopThroughCurrFile". click "Next".

	![](images/300/image021b.png)

- Next, choose stage file operation as "Read Entire file". Next, click on the pencil button next to box. This opens a new pop-up provide the details. Provide the details as shown in the below screenshot. For "Repeating Element" field, on the left hand side drag and drop ICSFile on to right side field as shown in the below screenshot. Enter "currentFile" for Current Element Name. Click on "save" or "Done". 

	![](images/300/image021c.png)
	![](images/300/image021d.png)
	![](images/300/image021e.png)

- The orchestration flow should now look like this:

	![](images/300/image021f.png)

- The next step is to Read through each file. From the right hand panel, by expanding "Actions" and locate Stage file. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image022.png)
	![](images/300/image022A.png)

- You are prompted to name the action. Call it "ReadCurrentFile". click "Next".

	![](images/300/image022b.png)

- Next, choose stage file operation as "Read Entire File". Next, click on the pencil button for "Specify the File Name" field. This opens a new pop-up provide the details. Provide the details as shown in the below screenshot. Drag and drop the "filename" from left hand panel on to right side Expression filed as shown. Click on "save" and hit "exit Expression Builder" to go back to previous screen. Next, click on the pencil button for "Specify the Directory to read from". This opens a new pop-up provide the details. Provide the details as shown in the below screenshot. Drag and drop the "directory" from left hand panel on to right side Expression filed as shown. Click on "save" and hit "exit Expression Builder" to go back to previous screen. The screens should look like one shown in screenshot and hit next.

	![](images/300/image022c.png)
	![](images/300/image022d.png)
	![](images/300/image022e.png)
	![](images/300/image022f.png)

- Next, enter the details for the endpoint and new schema options as shown and hit Next.

	![](images/300/image022g.png)

- Next, enter the details for the format definition as shown and hit Next.

	![](images/300/image022h.png)

- Check the details are right in the summary section and click "Done".

	![](images/300/image022i.png)

- The orchestration flow should now look like this:

	![](images/300/image022j.png)

- The next step is to write each file. From the right hand panel, by expanding "Actions" and locate Stage file. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image023.png)
	![](images/300/image023a.png)

- You are prompted to name the action. Call it "WriteCurrentFile". click "Next".

	![](images/300/image023b.png)

- Next, choose stage file operation as "Write File". Next, click on the pencil button for "Specify the File Name" field. This opens a new pop-up provide the details. Provide the details as shown in the below screenshot. Drag and drop the "filename" from left hand panel on to right side Expression filed as shown. Click on "save" and hit "exit Expression Builder" to go back to previous screen. Next, click on the pencil button for "Specify the output Directory". This opens a new pop-up provide the details. Enter the output directory in the expression field as shown in the screenshot. Click on "save" and hit "exit Expression Builder" to go back to previous screen. The screens should look like one shown in screenshot and hit next.

	![](images/300/image023c.png)
	![](images/300/image023d.png)
	![](images/300/image023e.png)
	![](images/300/image023f.png)

- Next, enter the details for the endpoint and new schema options as shown and hit Next.

	![](images/300/image023g.png)

- Next, enter the details for the format definition as shown and hit Next.

	![](images/300/image023h.png)

- Check the details are right in the summary section and click "Done".

	![](images/300/image023i.png)

- The orchestration flow should now look like this:

	![](images/300/image023j.png)

- Next step is to map the data between read and write file. Right click on the Mapping component as shown below. Clcik on the pencil icon. This opens up the mapping window.

	![](images/300/image024.png)

- Next, drag and drop the "C6" label under Entry on the left hand side "Source"  to "C6" label under entry "Entry" on the right side "Target" as shown below.

	![](images/300/image025.png)

- Next, on the right side "Target" click on "C6" under "mapping" as shown below. It opens up the window to edit mapping.

	![](images/300/image026.png)

- Next, on the right side hamburger menu click on "Actions". Delete the mapping as shown below.

	![](images/300/image027.png)

- Edit the mapping value to 'USD' as shown below. Click on "save" and close.

	![](images/300/image028.png)

- Finally the mapping should look like this. Validate and hit close. Go back and correct if it pops any errors.

	![](images/300/image029.png)

- The orchestration flow should now look like this:

	![](images/300/image030.png)

- The next step is to zip the updated files. From the right hand panel, by expanding "Actions" and locate Stage file. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image031.png)
	![](images/300/image031a.png)

- You are prompted to name the action. Call it "ZipUpdatedFiles". click "Next".

	![](images/300/image031b.png)

- Next, choose stage file operation as "Zip Files". Next, click on the pencil button for "Specify the File Name" field. This opens a new pop-up provide the details. Provide the details as shown in the below screenshot. Click on "save" and hit "exit Expression Builder" to go back to previous screen. Next, click on the pencil button for "Specify the Directory to read from". This opens a new pop-up provide the details. Provide the details as shown in the below screenshot. Click on "save" and hit "exit Expression Builder" to go back to previous screen. The screens should look like one shown in screenshot and hit next.

	![](images/300/image031c.png)
	![](images/300/image031d.png)
	![](images/300/image031e.png)
	![](images/300/image031f.png)

- Check the details are right in the summary section and click "Done".

	![](images/300/image031g.png)

- The orchestration flow should now look like this:

	![](images/300/image031h.png)

- The next step is to Send the updated files to ERP Cloud. We will use the ERP adapter to connect to ERP Cloud. From the right hand panel, select the ERP Adapter you had created in Lab 200. Drag and drop the component to the orchestration flow digram, as follows:

	![](images/300/image032.png)
	![](images/300/image032a.png)

- You are prompted to name the action. Call it "SendToERPCloud". Choose "Import Data into Financials Cloud Apllication" as the action endpoint. click "Next".

	![](images/300/image032b.png)

- Next, choose the operations as shown below. The screen should look like one shown in screenshot and hit next.

	![](images/300/image032c.png)

- Set the email notification for the job submission. Once done hit Next as shown below.

	![](images/300/image032d.png)

- Check the details are right in the summary section and click "Done".

	![](images/300/image032e.png)

- The orchestration flow should now look like this:

	![](images/300/image032f.png)

- Next step is to map the data between zipped files and files to be sent to ERP. Right click on the Mapping component as shown below. Clcik on the pencil icon. This opens up the mapping window.

	![](images/300/image033.png)

- Next, drag and drop the "FileReference" under ICSFile and all the Properties values under "Properties" in the source section on left to its corresponding matching fields on the right side under Target. The mapping should look like as shown below. Validate and hit close. Go back and correct if it pops any errors.

	![](images/300/image034.png)

- The orchestration flow should now look like this:

	![](images/300/image035.png)

- The next and final step is to add an tracking field for monitoring the integration flow. This wll help individual instances to be tracked. On the right hand side, click on the hamburger menu and click on tracking.

	![](images/300/image036.png)

- It opens up a window to add a field for tracking. Drag and drop the "startTime" field from source on the left to right side as shown below. Click on Done.

	![](images/300/image036a.png)

### **STEP 4**: Completed Integration

## Checking Your Integration

- When complete, the entire integration flow should look like this:

	![](images/300/image105.png)

- Save the integration and close to go back to Integration page and stay on the page to continue working on next lab.

	![](images/300/image105a.png)

- Congratulations. Your flow is ready to tested. Save the integration and close 
