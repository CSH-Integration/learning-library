# CSH Campaign Assets 2018: File Transfer with Oracle Integration Cloud

![](images/300/Lab300_title.png)

Updated: 11-Mar-2018

## Introduction

This is the third of several labs that are part of the **CSH Campaign Assets 2018: File Transfer with Oracle Integration Cloud**. This workshop will demonstrate how to read an opaque file from a *inbound* directory and write the file to an *upload* directory in a scheduled orchestrated integration. 

In this lab, you will learn how to create a basic File Transfer integration, using a scheduled orchestration. This integration will use the FTP connection creation in the previous lab (200).

***To log issues***, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives

- Create your first integration to transfer a file from an inbound to an outbound folder.

## Required Artifacts

-   The following lab and an Oracle Public Cloud account that will be supplied by your instructor.

# Create a New Integration
Connections allow Integration Cloud to interact with an application instance. A connection is required for every application instance that participates in an integration. In this lab, you will create one connection - for an FTP folder using the FTP adapter. 

## Create the Integration

### **STEP 1**:  Create a scheduled orchestrated integration

- Start **Integration Cloud** and click on **Integrations**.

    ![](images/300/Lab300_001.png)    

- In the resulting **Designer** navigation pane, click **Integrations** (default selection).

    ![](images/300/Lab300_002.png)    

- In the **Integrations** pane, click on the **Create** button in the upper right.

    ![](images/300/Lab300_003.png)    

- In the **Create Integration - Select a Style/Pattern** popup, select the **Orchestration**

    ![](images/300/Lab300_004.png)    

- Fill in the **Create New Integration** form with the following information:

  **What triggers this integration?**: `Schedule`	

  **What do you want to call your integration?**: `FileTransfer_XX` (where `XX` should be your initials)

  **Identifier**: Auto generated (keep default value)

  **What does this integration do?**: `This is a File Transfer integration to read an opaque file from an inbound directory and write the file to an upload directory.`

  Click **Create** to initialize and open the integration.

  ![](images/300/Lab300_005.png)   


## Configure the FTP Connections (ReadFile & WriteFile)

Let's start with the **FTP Adapter** for the **Read File** operation. We will configure a read file in binary mode from an inbound directory of the server specified in the **Connections** page. No schema is defined for this file transfer, so it is treated as an attachment.

- In the **Invokes** panel, expand the **FTP** heading, and find your connection, under **FTPConnection_XX**

  ![](images/300/Lab300_006.png)   

- Drag and drop your connection **FTPConnection_XX** in to the circle with the plus sign. You will see the plus sign twirling when ready to drop.

  ![](images/300/Lab300_007.png)   

- In the **Basic Info** page, enter `ReadFile` for endpoint name and click **Next**.
  
- In the **Operations** page, enter the following information and click **Next**.
  
  - **Select Operation**: `Read a File`
  
  - **Select a Transfer Mode**: `Binary`

  - **Input Directory**: `/`

  - **File Name**: `1KB.zip`

- In the **Schema** page, enter the following information and click **Next**.

  **Do you want to define a schema for this endpoint?**: `No`
  
- Validate your values in the **Summary Page**.

  ![](images/300/Lab300_008.png)   
  
- Click **Done**.

- Click **Save** on the main canvas to save your work.

Let's continue with the **FTP Adapter** for the **Write File** operation. We will configure a write file to the outbound directory on the same server specified in the **Connections** page, that matches the file name pattern of `XX_1KB%yyMMddHHmmssSS%.zip`.

- In the **Invokes** panel, expand the **FTP** heading, and find your connection, under **FTPConnection_XX**

  ![](images/300/Lab300_006.png)   

- Drag and drop your connection **FTPConnection_XX** below the **ReadFile** connection in to the circle with the plus sign. You will see the plus sign twirling when ready to drop.

  ![](images/300/Lab300_009.png)   

- In the **Basic Info** page, enter `WriteFile` for endpoint name and click **Next**.

- In the **Operations** page, enter the following information and click **Next**.
  
  -  **Select Operation**: `Write File`
  
  - **Select a Transfer Mode**: `ASCII`

  - **Output Directory**: `/upload`

  - **File Name Pattern**: `XX_1KB%yyMMddHHmmssSS%.zip` (where `XX` should be your initials)

  - **Enable PGP Security**: `No`

  - **Do you want to define a schema for this endpoint?**: `No`
  
- Validate your values in the **Summary Page**.

  ![](images/300/Lab300_010.png)   

- Click **Done**.

- Click **Save** on the main canvas to save your work.

Observe that the orchestration's design palette is populated with the Connections **ReadFile** and **WriteFile** just created along with their mapping.

## Create Logging Messages
A logging message is created to indicate that the file name has been read. Another logging message is created to indicate the file name has been uploaded to the `/upload` directory Both messages are logged to the activity stream.

Let's start with the first **Logger** action to indicate a file read has occurred.

- In the **Action** panel,  drag and drop the **Logger** action after the **ReadFile** connection in to the circle with the plus sign. You will see the plus sign twirling when ready to drop.

  ![](images/300/Lab300_011.png)   

- In the **Create Action** wizard, enter `LogReadFileName` for **Name** and click **Create**.
 
- In the **Logger Action** page, select `Always` under Log and click on the **Expression Builder** (pencil icon)

  ![](images/300/Lab300_012.png)   

We will create a new expression that will show the file name in the logger.  

- Go to the **Components** pane, and search for the **concat** function. Enter `concat`and click **Enter**.

  ![](images/300/Lab300_013.png)   

- Drag and drop the **concat** function in to the **Expression** text area.

  ![](images/300/Lab300_014.png)   

- Replace the **string1** of the expression with the static value (including quotes) `"Filename is: "`. 

- We will copy the file name variable as the second string parameter. Select the **string2** text in the expression, and press **Delete**. Leave the cursor where the second parameter should be entered.

  ![](images/300/Lab300_015.png)   

- In the **Source** pane, expand $ReadFile > $SynchReadFileResponse > FileReadResponse > [Load More] > FTPResponseHeader. Make sure the cursor is in the position of the second parameter. Select the **fileName** element and click on the right arrow icon ![](images/300/Lab300_expression-copy-icon.png) to copy it as parameter in the **concat** function.  

  ![](images/300/Lab300_016.png)   

- Click on **Validate**, then **Close** in the upper right to exit the  **Log Message** expression builder canvas.

  ![](images/300/Lab300_017.png)   

- Click on **Validate**, then **Close** in the upper right to exit the **Logger Action** canvas.

  ![](images/300/Lab300_018.png)   

- Save the progress of your orchestration by clicking on the **Save** icon in the upper right of the design window.

Let's continue with the next **Logger** action to log the write file info. 

- In the **Action** panel,  drag and drop the **Logger** action after the **WriteFile** connection in to the circle with the plus sign. You will see the plus sign twirling when ready to drop.

  ![](images/300/Lab300_019.png)   

- In the **Create Action** wizard, enter `LogWriteFileInfo` for **Name** and click **Create**.

- In the **Logger Action** page, select `Always` under Log and click on the **Expression Builder** (pencil icon)

  ![](images/300/Lab300_012.png)   

We will create a new expression that will show the file info in the logger.  

- Go to the **Components** pane, and search for the **concat** function. Enter `concat`and click **Enter**.

  ![](images/300/Lab300_013.png)   

- Drag and drop the **concat** function in to the **Expression** text area.

  ![](images/300/Lab300_014.png)   

- Replace the **string1** of the expression with the static value (including quotes) `"The file "`. 

- We will copy the file name variable as the second string parameter. Select the **string2** text in the expression, and press **Delete**. Leave the cursor where the second parameter should be entered.

  ![](images/300/Lab300_020.png)   

- In the **Source** pane, expand WriteFile > WriteFileResponse > FTPWriteResponse. Make sure the cursor is in the position of the second parameter. Select the **fileName** element and click on the right arrow icon ![](images/300/Lab300_expression-copy-icon.png) to copy it as parameter in the **concat** function.  

  ![](images/300/Lab300_021.png)   

- Add a third parameter by inserting the following static value (including comma and quotes) at the end of the Expression: `, "has been uploaded to "`. 

  ![](images/300/Lab300_022.png)   

- Add a fourth and final parameter, using the **directory** variable. Start by adding a comma and space (`, `) at the end of the expression and keep the cursor on that last position, just before the closing parenthesis bracket.  

- In the **Source** pane, expand WriteFile > WriteFileResponse > FTPWriteResponse. Make sure the cursor is in the position of the second parameter. Select the **directory** element and click on the right arrow icon ![](images/300/Lab300_expression-copy-icon.png) to copy it as parameter in the **concat** function.  

  ![](images/300/Lab300_023.png)   

- Click on **Validate**, then **Close** in the upper right to exit the  **Log Message** expression builder canvas.

  ![](images/300/Lab300_024.png)   

- Click on **Validate**, then **Close** in the upper right to exit the **Logger Action** canvas.

  ![](images/300/Lab300_025.png)   

- Save the progress of your orchestration by clicking on the **Save** icon in the upper right of the design window.

## Configure an Assign action
An assign action is configured to assign variables for the file name and file size. This enables you to track issues based on filename and size. 

- In the **Action** panel, drag and drop the **Assign** action after the **LogReadFileName** logger in to the circle with the plus sign. You will see the plus sign twirling when ready to drop. 

  ![](images/300/Lab300_026.png)   

- In the **Create Action** wizard, enter `AssignTrackingVariable` for **Name** and click **Create**.

- In the **Assign** page, click on the ![](images/300/Lab300_assign-add-icon.png) icon to configure the first variable.

- Assign the following information tot the first variable.

  - **Variable**: Select the variable called `tracking_var_2` from the drop down
    
  - **Data Type**: `simple` (default)

  - **Value**: 
    - Click on the pencil button to open the Expression editor. 

    - Go to the **Components** pane, and search for the **concat** function. Enter `concat`and click **Enter**.
    ![](images/300/Lab300_013.png)
    - Drag and drop the **concat** function in to the **Expression** text area.
    ![](images/300/Lab300_014.png)
    - Replace the **string1** of the expression with the static value (including quotes) `"Filename: "`.

    - Copy the file name variable as the second string parameter. Select the **string2** text in the expression, and press **Delete**. Leave the cursor where the second parameter should be entered.

    - In the **Source** pane, expand **$ReadFile > SynchReadFileResponse > FileReadResponse > ICSFile > [Load More] > Properties > [Load More]**. Make sure the cursor is in the position of the second parameter. Select the `filename` element and click on the right arrow icon ![](Lab300_expression-copy-icon.png) to copy it as parameter in the **concat** function.

    ![](images/300/Lab300_027.png)

    - Click on **Validate**, then **Close** in the upper right to exit the **tracking_var_2** expression builder canvas.

    ![](images/300/Lab300_028.png)

-  Next, click again on the ![](images/300/Lab300_assign-add-icon.png) icon to configure the second variable.

- Assign the following information tot the second variable.

  - **Variable**: Select the variable called `tracking_var_3` from the drop down
    
  - **Data Type**: `simple` (default)

  - **Value**: 
    - Click on the pencil button to open the Expression editor. 

    - Go to the **Components** pane, and search for the **concat** function. Enter `concat`and click **Enter**.
    ![](images/300/Lab300_013.png)
    - Drag and drop the **concat** function in to the **Expression** text area.
    ![](images/300/Lab300_014.png)
    - Replace the **string1** of the expression with the static value (including quotes) `"Filesize: "`.

    - Copy the file size variable as the second string parameter. Select the **string2** text in the expression, and press **Delete**. Leave the cursor where the second parameter should be entered.

    - In the **Source** pane, expand **$ReadFile > SynchReadFileResponse > FileReadResponse > ICSFile > [Load More] > Properties > [Load More]**. Make sure the cursor is in the position of the second parameter. Select the `filesize` element and click on the right arrow icon ![](Lab300_expression-copy-icon.png) to copy it as parameter in the **concat** function.

    ![](images/300/Lab300_029.png)

    - Click on **Validate**, then **Close** in the upper right to exit the **tracking_var_3** expression builder canvas.

    ![](images/300/Lab300_030.png)

- Verify the two variables. Next, click on **Validate**, then **Close** in the upper right to exit the **AssignTrackingVariable** canvas.

    ![](images/300/Lab300_031.png)

- Save the progress of your orchestration by clicking on the **Save** icon in the upper right of the design window.

## Map the data
The mapping objects were automatically created when we added the connections. We will configure a mapping action to connect the fields to the **WriteFile** connection. For this lab, only the **Map to WriteFile** mapping is required. 

First, remove the ReadFile mapping.

- Click on the **Map to ReadFile** mapping. 

- Next, click on the **pencil icon** to edit the mapping. Then, click on **Delete**. 

    ![](images/300/Lab300_032.png)

- In the **Delete Map Action?** dialog, click **Delete**.

   ![](images/300/Lab300_033.png)

Now let's complete the WriteFile mapping. We only need to map the **FileReference** variable.

- Click on the **Map to WriteFile** mapping, then click on the **pencil icon** to edit the mapping.

  ![](images/300/Lab300_034.png)

- In the **Source** variable section, click on **$ReadFile > SyncReadFileResponse > FileReadResponse > ICSFile > FileReference**.

- Click on the little circle to the right of the **FileReference** source variable and then drag it on top of the little circle just to the left of the **FileReference** target variable under **WriteFile > ICSFile**.

  ![](images/300/Lab300_035.png)

-  Select the **Validate** button in the upper right of the mapping editor. After validating, select the **Close** button also in the upper right

  ![](images/300/Lab300_036.png)


## Track Fields


## Activate the Integration


