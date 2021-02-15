# DP 200 - Implementing a Data Platform Solution
# Lab 7 - Securing Azure Data Platforms

**Estimated Time**: 75 minutes

**Lab files**: The files for this lab are located in the _C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200.8_ folder.

## Lab overview

The students will be able to describe and document the different approaches to security that can be taken to provide defence in depth. This will involve the student documenting the security that has been set up so far in the course. It will also enable the students to identify any gaps in security that may exists for AdventureWorks.

## Lab objectives
  
After completing this lab, you will be able to:

1. Explain Security
1. Describe key security components
1. Secure Storage Accounts and Data Lake Storage
1. Secure Data Stores
1. Secure Streaming Data

## Scenario
  
As a senior data engineer within AdventureWorks, you are responsible for ensuring that your data estate is secured. You are performing a security check of your current infrastructure to ensure that you have diligently placed security where it is required. This check should be a holistic check of all the services and data that you have created so far, and an identification of any gaps that there may be in the configuration of the security. 

You have also been asked to tighten up the security of the SQL Database DeptDatabasesxx and have been asked to setup auditing against the database so that you can monitor access to the database. Furthermore, you have learned that that the Manage permission for your event hub is not restrictive enough, and you want to remove this permission.

At the end of this lab, you will have:

1. Explained Security
1. Described key security components
1. Secured Storage Accounts and Data Lake Storage
1. Secured Data Stores
1. Secured Streaming Data

> **IMPORTANT**: As you go through this lab, make a note of any issue(s) that you have encountered in any provisioning or configuration tasks and log it in the table in the document located at _C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\DP-200-Issues-Doc.docx_. Document the Lab number, note the technology, Describe the issue, and what was the resolution. Save this document as you will refer back to it in a later module.

## Exercise 1: An introduction to security

Estimated Time: 15 minutes

Group exercise
  
The main task for this exercise are as follows:

1. Security as a layered approach.

1. The instructor will discuss the findings with the group.

### Task 1: Security as a layered approach.

1. Before starting just to familiarize, we will be using deployment id for naming convention where xxxxxx will be asked to replace with deployment id and it can be found from the environment details tab from the right side of your environment.

    ![](Linked_Image_Files/deployment-ID.png)

1. From the lab virtual machine, open up the file **DP-200-Lab08-Ex01.docx** from the **C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200.8** folder.This file will open in wordpad.

1. From the course content, case study and the scenarios taken in the course so far, spend **10 minutes** in a group identifying the layers of security that you have impacted so far to secure AdventureWorks in the labs. Find three examples.

### Task 2: Discuss the findings with the Instructor

1. The instructor will stop the group to discuss the findings.

> **Result**: After you completed this exercise, you have created a Microsoft Word document that contains at least three examples of how you have implemented security at Adventureworks and which layer of security you have impacted.

## Exercise 2: Securing Storage Accounts and Data Lake Storage
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Determining the appropriate security approach for Azure Blob

1. Discuss the findings with the Instructor

### Task 1: Determining the appropriate security approach for Azure Blob

1. You have been approached by your in-house web developer to help give access to a third party web design company to the web images that are in the awsastudxx storage account. As a senior data engineer within AdventureWorks, what steps would you need to take to ensure this can happen while applying the correct due diligence.

1. From the lab virtual machine, start **Microsoft Word**, and open up the file **DP-200-Lab08-Ex03.docx** from the **Allfiles\Labfiles\Starter\DP-200.8** folder.

### Task 2: Discuss the findings with the Instructor

1. The instructor will stop the group to discuss the findings.

> **Result**: After you completed this exercise, you have created a Microsoft Word document that contains the steps that you would take to provide secure access to a Blob storage account to a third-party web development company.

## Exercise 3: Securing Data Stores
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Enabling Auditing

1. Query the Database

1. View the Audit log

### Task 1: Enabling Auditing

1. In the Azure portal, in the blade, click **Resource groups**, and then click **awrgstud-deploymentID**, and then click on **AdventureWorksLT**.

1. In the **sqlservice-deploymentId/AdventureWorksLT** database screen, click on the **Auditing** blade.

1. Under **Enable Azure SQL Auditing**, click on the **ON** button.

1. Select the checkbox next to **Storage**.

1. Click on **Storage Details - Configure**.

    ![](Linked_Image_Files/lab7-ex3-task1-step5.png)

1. In the **Storage Setting** screen, click **Subscription - change storage subscription**, and then click your subscription.

1. In the **Storage Setting** screen, click **Storage Settings - Configure required settings**. In the **Choose storage account** screen, click **awsastud(deploymentId)**

    ![](Linked_Image_Files/lab7-ex3-task1-step7_1.png)
    
    ![](Linked_Image_Files/lab7-ex3-task1-step7_2.png)

1. In the **Retention Days** text box, type **90**, and then click on **OK**.

    ![Configuring Auditing in the Azure Portal](Linked_Image_Files/lab7-ex3-task1-step8.png)

1. Click on **Save**.

1. In the Azure portal, in the search blade, search for the sql servers and then click on **sqlservice-DeploymentID**, and then click on Auditing Under Security.

1. Under **Enable Azure SQL Auditing**, click on the **ON** button, then select storage account box and Select the same storage account that you configured for database auditing in the beginning of this task.

    ![](Linked_Image_Files/dp-200module7-newimage.png)
    
1. Click on **Save**.

### Task 2: Query the database

1. In the Azure portal, in the blade, click Resource groups, select **awrgstud-deploymentID**, and then click on **sqlservice-deploymentId**.

    ![](Linked_Image_Files/lab7-ex3-task2-step1.png)

1. From the left navigation menu under **Settings** select **Properties**. Copy the **"Server name"** and paste it into Notepad.

    ![](Linked_Image_Files/lab7-ex3-task2-step2.png)

1. On the windows desktop, click on the **Start**, and type **"SQL Server"** and then click on **Microsoft SQL Server Management Studio 18**

    ![](Linked_Image_Files/lab7-ex3-task2-step3.png)

1. In the **Connect to Server** dialog box, fill in the following details
    - Server Name: **sqlservice-deploymentID.database.windows.net** (paste the value that you copied in the previous step).
    - Authentication: **SQL Server Authentication**
    - Username: **sqladmin**
    - Password: **P@ssw0r**

    ![](Linked_Image_Files/lab7-ex3-task2-step4.png)

1. In the **Connect to Server** dialog box, click **Connect** 

> **Note**: An error message is returned as the password is incorrect. Type in the correct password of **P@Ssw0rd**.

   ![](Linked_Image_Files/lab7-ex3-task2-step5.png)

1. Type in the correct password of **Pa55w.rd**

1. In **SQL Server Management Studio**, in Object Explorer, expand **AdventureWorksLT**, and then expand **Tables**.

1. Right click [SalesLT].[Customers] and then click **Select Top 1000 Rows**

    ![](Linked_Image_Files/lab7-ex3-task2-laststep.png)

### Task 3: View the Audit Log

1. Return to the Azure Portal. In the AdventureWorksLT (sqlservice-deploymentID/AdventureWorksLT) - Auditing screen, click on **View Audit Logs**

    ![](Linked_Image_Files/lab7-ex3-task3-step1.png)

1. Note in the **Audit records** log file the **Failed Authentication** record. Close down the **Audit records** screen. (**Note :-** Please scroll down through the logs to find the failed record.)

    ![Viewing Audit records in the Azure Portal](Linked_Image_Files/lab7-lastimage.png)

> **Result**: After you completed this exercise, you have enabled database auditing and verified that the auditing works.

## Exercise 4: Securing Streaming Data
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Changing Event Hub Permissions

### Task 1: Changing Event Hub Permissions

1. In the Azure portal, in the blade, click **Resource groups**, and then click **awrgstud-deploymentID**, and then click on **phoneanalysis-ehn-deploymentID**.

1. In the Azure portal, in the **phoneanalysis-ehn-deploymentID**. Scroll to the bottom of the window, and click on **co-phoneanalysis-eh** event hub.

    ![](Linked_Image_Files/lab7-lastimage2.png)

1. To grant access to the event hub, click **Shared access policies**.

1. Under the **co-phoneanalysis-eh - Shared access policies** screen, click on **phoneanalysis-eh-sap**.

    ![](Linked_Image_Files/lab7-lastimage3.png)

1. Click on the checkbox next to the **Manage** permissions to remove it, and then click **Save**.

    ![](Linked_Image_Files/lab7-lastimage4.png)

1. In the Azure portal, in the blade, click **Home**,

> **Result**: After you completed this exercise, you modified the security of an Event Hub Shared Access Policy.
