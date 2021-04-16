# DP 200 - Implementing a Data Platform Solution
# Lab 7 - Securing Azure Data Platforms

**Estimated Time**: 75 minutes

**Lab files**: The files for this lab are located in the _C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200.8_ folder.

## Lab overview

The students will be able to describe and document the different approaches to security that can be taken to provide defence in depth. This will involve the student documenting the security that has been set up so far in the course. It will also enable the students to identify any gaps in security that may exists for AdventureWorks.

## Lab objectives
  
After completing this lab, you will be able to:

1. Explain Security
2. Describe key security components
3. Secure Storage Accounts and Data Lake Storage
4. Secure Data Stores
5. Secure Streaming Data

## Scenario
  
As a senior data engineer within AdventureWorks, you are responsible for ensuring that your data estate is secured. You are performing a security check of your current infrastructure to ensure that you have diligently placed security where it is required. This check should be a holistic check of all the services and data that you have created so far, and an identification of any gaps that there may be in the configuration of the security. 

You have also been asked to tighten up the security of the SQL Database DeptDatabasesxx and have been asked to setup auditing against the database so that you can monitor access to the database. Furthermore, you have learned that that the Manage permission for your event hub is not restrictive enough, and you want to remove this permission.

At the end of this lab, you will have:

1. Explained Security
2. Described key security components
3. Secured Storage Accounts and Data Lake Storage
4. Secured Data Stores
5. Secured Streaming Data

> **IMPORTANT**: As you go through this lab, make a note of any issue(s) that you have encountered in any provisioning or configuration tasks and log it in the table in the document located at _C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\DP-200-Issues-Doc.docx_. Document the Lab number, note the technology, Describe the issue, and what was the resolution. Save this document as you will refer back to it in a later module.

## Exercise 1: An introduction to security

Estimated Time: 15 minutes

Group exercise
  
The main task for this exercise are as follows:

1. Security as a layered approach.

2. The instructor will discuss the findings with the group.

### Task 1: Security as a layered approach.

1. Before starting just to familiarize, we will be using deployment id for naming convention where xxxxxx will be asked to replace with deployment id and it can be found from the environment details tab from the right side of your environment.

    ![](Linked_Image_Files/deployment-ID.png)

2. From the lab virtual machine, open up the file **DP-200-Lab08-Ex01.docx** from the **C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200.8** folder.This file will open in wordpad.

3. From the course content, case study and the scenarios taken in the course so far, spend **10 minutes** in a group identifying the layers of security that you have impacted so far to secure AdventureWorks in the labs. Find three examples.

### Task 2: Discuss the findings with the Instructor

1. The instructor will stop the group to discuss the findings.

> **Result**: After you completed this exercise, you have created a Microsoft Word document that contains at least three examples of how you have implemented security at Adventureworks and which layer of security you have impacted.

## Exercise 2: Securing Storage Accounts and Data Lake Storage
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Determining the appropriate security approach for Azure Blob

2. Discuss the findings with the Instructor

### Task 1: Determining the appropriate security approach for Azure Blob

1. You have been approached by your in-house web developer to help give access to a third party web design company to the web images that are in the awsastudxx storage account. As a senior data engineer within AdventureWorks, what steps would you need to take to ensure this can happen while applying the correct due diligence.

2. From the lab virtual machine, start **Wordpad**, and open up the file **DP-200-Lab08-Ex03.docx** from the **C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200.8** folder.

### Task 2: Discuss the findings with the Instructor

1. The instructor will stop the group to discuss the findings.

> **Result**: After you completed this exercise, you have created a Microsoft Word document that contains the steps that you would take to provide secure access to a Blob storage account to a third-party web development company.

## Exercise 3: Securing Data Stores
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Enabling Auditing

2. Query the Database

3. View the Audit log

### Task 1: Enabling Auditing

1. In the Azure portal, in the blade, click **Resource groups**, and then click **awrgstud-deploymentID**, and then click on **AdventureWorksLT**.

2. In the **sqlservice-deploymentId/AdventureWorksLT** database screen, click on the **Auditing** blade.

    ![](Linked_Image_Files/lab7-ex3-task1-step2.png)
    
3. Perform the following steps:

  - **Enable Azure SQL Auditing** - Click on the toggle button to enable Auditing
  - Select the checkbox next to **Storage**.
  - **Subscription** - Select your subscription from the drop down
  - **Storage Account** - Select your storage account(i.e., **awsastud(deploymentId)**) from the drop down
  - Click on **Advanced properties**
  - In the **Retention Days** text box, type **90**
  - **Storage access key** - Set to **Primary**
  - Click on **Save**

4. In Azure portal, in the search blade, search for the sql servers and then click on **sqlservice-DeploymentID**, and then click on **Auditing** Under Security.

5. Perform the following steps:

  - **Enable Azure SQL Auditing** - Click on the toggle button to enable Auditing
  - Select the checkbox next to **Storage**.
  - **Subscription** - Select your subscription from the drop down
  - **Storage Account** - Select your storage account(i.e., **awsastud(deploymentId)**) from the drop down
  - Click on **Advanced properties**
  - In the **Retention Days** text box, type **90**
  - **Storage access key** - Set to **Primary**
  - Click on **Save**

    ![](Linked_Image_Files/dp-200mod7-updatedimage.png)
    

### Task 2: Query the database

1. In the Azure portal, in the blade, click Resource groups, select **awrgstud-deploymentID**, and then click on **sqlservice-deploymentId**.

    ![](Linked_Image_Files/lab7-ex3-task2-step1.png)

2. From the Overview page navigation, copy the **"Server name"** and paste it into Notepad.

    ![](Linked_Image_Files/lab7-ex3-task2-step2.png)

3. On the windows desktop, click on the **Start**, and type **"SQL Server"** and then click on **Microsoft SQL Server Management Studio 18**

    ![](Linked_Image_Files/lab7-ex3-task2-step3.png)

4. In the **Connect to Server** dialog box, fill in the following details
    - Server Name: **sqlservice-deploymentID.database.windows.net** (paste the value that you copied in the previous step).
    - Authentication: **SQL Server Authentication**
    - Username: **sqladmin**
    - Password: **P@ssw0r**

    ![](Linked_Image_Files/lab7-ex3-task2-step4.png)

5. In the **Connect to Server** dialog box, click **Connect** 

> **Note**: An error message is returned as the password is incorrect. Type in the correct password of **P@Ssw0rd**.

   ![](Linked_Image_Files/lab7-ex3-task2-step5.png)

6. Type in the correct password of **Pa55w.rd**

7. In **SQL Server Management Studio**, in Object Explorer, expand **AdventureWorksLT**, and then expand **Tables**.

8. Right click [SalesLT].[Customers] and then click **Select Top 1000 Rows**

    ![](Linked_Image_Files/lab7-ex3-task2-laststep.png)

### Task 3: View the Audit Log

1. Return to the Azure Portal. In the AdventureWorksLT (sqlservice-deploymentID/AdventureWorksLT) - Auditing screen, click on **View Audit Logs**

    ![](Linked_Image_Files/lab7-ex3-task3-step1.png)

2. Note in the **Audit records** log file the **Failed Authentication** record. Close down the **Audit records** screen. (**Note :-** Please scroll down through the logs to find the failed record.)

    ![Viewing Audit records in the Azure Portal](Linked_Image_Files/lab7-lastimage.png)

> **Result**: After you completed this exercise, you have enabled database auditing and verified that the auditing works.

## Exercise 4: Securing Streaming Data
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Changing Event Hub Permissions

### Task 1: Changing Event Hub Permissions

1. In the Azure portal, in the blade, click **Resource groups**, and then click **awrgstud-deploymentID**, and then click on **phoneanalysis-ehn-deploymentID**.

2. In the Azure portal, in the **phoneanalysis-ehn-deploymentID**. Scroll to the bottom of the window, and click on **co-phoneanalysis-eh** event hub.

    ![](Linked_Image_Files/up-lab7-lastimage3.png)

3. To grant access to the event hub, click **Shared access policies**.

4. Under the **co-phoneanalysis-eh - Shared access policies** screen, click on **phoneanalysis-eh-sap**.

    ![](Linked_Image_Files/lab7-lastimage3.png)

5. Click on the checkbox next to the **Manage** permissions to remove it, and then click **Save**.

    ![](Linked_Image_Files/lab7-lastimage4.png)

6. In the Azure portal, in the blade, click **Home**,

> **Result**: After you completed this exercise, you modified the security of an Event Hub Shared Access Policy.
