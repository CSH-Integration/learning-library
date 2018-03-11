# CSH Campaign Assets 2018: ICS File Transfer

![](images/200/Picture-lab.png)

Updated: 09-Mar-2018

## Introduction

This sample demonstrates how to read an opaque file from a "/" directory and write the file to an "/upload" directory in a scheduled orchestrated integration. An FTP Adapter reads the file from the / directory and another FTP Adapter writes the file to the /upload directory. An assign action is configured to assign variables for the file name and file size. A logging message is created to indicate that the file name has been read. The message is logged to the activity stream for viewing. You also track the integration and monitor message status.

 ![](images/sample/sample_001.png)

***To log issues***, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

**Complexity**
*Medium*

**Prerequisites**
*None*


## How To Activate

- In the navigation pane, click **Integrations**.
- In the row for the File Transfer sample, click the **Activate** icon, then click **Activate** when prompted.
    ![](images/sample/sample_002.png)

## Required Artifacts

- The following lab requires an Oracle Public Cloud account that will be supplied by your instructor. You will need to download and install latest version of Eclipse or used supplied compute VM. Instructions are found in the Student Guide.

# Create Initial Static Twitter Feed Service

## Explore Developer Cloud Service

### **STEP 1**: Review Agile Board

- This Lab assumes that you just completed Lab 100 and are still connected to the Oracle Cloud, that you're still in the Developer cloud Service Dashboard, and you're viewing the "Alpha Office Product Catalog Project". If for some reason that is not the case, follow the first several Steps of Lab 100 to once again view the Developer Cloud Service Console.

    ![](images/200/Picture10.5.png)  

- Although you will remain connected to the Oracle Cloud using the user account you were provided, you will take on the Persona of ***Bala Gupta*** as you perform the following steps.

    ![](images/bala.png)  

- Within the **Alpha Office Product Catalog Project**, click on **Agile** found on the left hand navigation.

    ![](images/200/Picture11.png)  



### **STEP 17**: Create New Twitter App

To generate the unique twitter credentials for our microservices, we need to sign in to twitter and create a new application for this project, then generate access tokens for it.

- Navigate to https://apps.twitter.com. Click on the **Sign In** link.

    ![](images/200/image119.png)  

- If you are already a twitter user, **Log In** using your twitter credentials. Otherwise, click on the **Sign up Now** link

    ![](images/200/image120.png)  

- Once logged in, click on the **Create New App** button.

    ![](images/200/image121.png)  

- **Enter the following** and Click on the **Create your Twitter application** button. When entering the Application Name, append something unique to the Name’s end. E.g. your initials or name:

  **Name:** `JavaTwitterMicroservice<UniqueName>`

  **Description:** `A Twitter Feed Microservice`

  **Website:** `https://cloud.oracle.com/acc`

  **Developer Agreement:** Click `Yes`

    ![](images/200/image122.png)  

- Click on the **Keys and Access Tokens** tab.

    ![](images/200/image123.png)  



