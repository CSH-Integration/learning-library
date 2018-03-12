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
  
  **Select Operation**: `Read a File`
  
  **Select a Transfer Mode**: `Binary`

  **Input Directory**: `/`

  **File Name**: `1KB.zip`

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
  
  **Select Operation**: `Write File`
  
  **Select a Transfer Mode**: `ASCII`

  **Output Directory**: `/upload`

  **File Name Pattern**: `XX_1KB%yyMMddHHmmssSS%.zip` (where `XX` should be your initials)

  **Enable PGP Security**: `No`

  **Do you want to define a schema for this endpoint?**: `No`
  
- Validate your values in the **Summary Page**.

  ![](images/300/Lab300_010.png)   

- Click **Done**.

- Click **Save** on the main canvas to save your work.

## Create a Logging Message



## Configure an Assign action


## Map the data


## Track Fields


## Activate the Integration


