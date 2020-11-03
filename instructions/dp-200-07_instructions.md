# DP 200 - Implementing a Data Platform Solution
# Lab 6 - Orchestrating Data Movement with Azure Data Factory

**Estimated Time**: 70 minutes

## Lab overview

In this module, students will learn how Azure Data factory can be used to orchestrate the data movement from a wide range of data platform technologies. They will be able to explain the capabilities of the technology and be able to set up an end to end data pipeline that ingests data from SQL Database and load the data into Azure Synapse Analytics. The student will also demonstrate how to call a compute resource.

## Lab objectives
  
After completing this lab, you will be able to:

1. Setup Azure Data Factory
1. Ingest data using the Copy Activity
1. Use the Mapping Data Flow task to perform transformation
1. Perform transformations using a compute resource

## Scenario
  
You are assessing the tooling that can help with the extraction, load and transforming of data into the data warehouse, and have asked a Data Engineer within your team to show a proof of concept of Azure Data Factory to explore the transformation capabilities of the product. The proof of concept does not have to be related to AdventureWorks data, and you have given them freedom to pick a dataset of thier choice to showcase the capabilities.

In addition, the Data Scientists have asked to confirm if Azure Databricks can be called from Azure Data Factory. To that end, you will create a simple proof of concept Data Factory pipeline that calls Azure Databricks as a compute resource.

At the end of this lab, you will have:

1. Setup Azure Data Factory
1. Ingested data using the Copy Activity
1. Used the Mapping Data Flow task to perform transformation
1. Performed transformations using a compute resource

> **IMPORTANT**: As you go through this lab, make a note of any issue(s) that you have encountered in any provisioning or configuration tasks and log it in the table in the document located at C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200-Issues-Doc.docx_. Document the Lab number, note the technology, Describe the issue, and what was the resolution. Save this document as you will refer back to it in a later module.

## Exercise 1: Setup Azure Data Factory

Estimated Time: 15 minutes

Individual exercise

The main task for this exercise are as follows:

1. Setup Azure Data Factory

### Task 1: Setting up Azure Data Factory.

1. Before starting just to familiarize, we will be using deployment id for naming convention where xxxxxx will be asked to replace with deployment id and it can be found from the environment details tab from the right side of your environment.

1. Create your data factory: Use the [Azure Portal](https://portal.azure.com) to create your Data Factory. 

1. In Microsoft Edge, go to the Azure portal tab, click on the **+ Create a resource** icon, type **factory**, and then click **Data Factory** from the resulting search, and then click **Create**.

1. In the New Data Factory screen, create a new Data Factory with the following options, then click **Create**:
    - **Name**: data-factory-xxxxxx, where xxxxxx is the deployment id 
    - **Version**: V2
    - **Subscription**: Your subscription
    - **Resource group**: awrgstud-deploymentId
    - **Location**: east us
    - click on next : Git Configuration
    - **Configure Git later**: checked
    - Leave other options to their default settings
    - Click **Review+Create** and then Click Create

        ![](Linked_Image_Files/lab6_1.jpg)
        
        ![](Linked_Image_Files/lab6_2.jpg)

    > **Note**: The creation of the Data Factory takes approximately 2 minute.

> **Result**: After you completed this exercise, you have created an instance of Azure Data Factory

## Exercise 2: Ingest data using the Copy Activity
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Add the Copy Activity to the designer

1. Create a new HTTP dataset to use as a source

1. Create a new ADLS Gen2 sink

1. Test the Copy Activity

### Task 1: Add the Copy Activity to the designer

1. On the deployment successful message, click on the button **Go to resource**.

    ![](Linked_Image_Files/lab6_3.jpg)

1. In the data-factory-deploymentId screen, in the middle of the screen, click on the button, **Author & Monitor**.

    ![](Linked_Image_Files/lab6_4.jpg)

1. **Open the authoring canvas** If coming from the ADF homepage, click on the **pencil icon** on the left sidebar or the **create pipeline button** to open the authoring canvas.

    ![](Linked_Image_Files/lab6_5.jpg)

1. **Create the pipeline** Click on the **+** button in the Factory Resources pane and select Pipeline

    ![](Linked_Image_Files/lab6_6.jpg)

1. **Add a copy activity** In the Activities pane, expand the Move and Transform and drag the Copy Data activity onto the pipeline canvas(blank side).

    ![](Linked_Image_Files/lab6_7.jpg)

    ![Adding the Copy Activity to Azure Data Factory in the Azure Portal](Linked_Image_Files/M07-E02-T01-img01.png)


### Task 2: Create a new HTTP dataset to use as a source

1. Click on the copy data activity tab, and below navigate to the **Source** tab of the Copy activity settings, click **+ New**

    ![](Linked_Image_Files/lab6_8.jpg)

1. In the **New dataset** blade, In search column of data store list, search for **HTTP** select the **HTTP** tile and click continue

    ![](Linked_Image_Files/lab6_9.jpg)

1. In the file format list, select the **DelimitedText** format tile and click continue

    ![](Linked_Image_Files/lab6_10.jpg)

1. In Set Properties blade, give your dataset an understandable name such as **HTTPSource** and click on the **Linked Service** dropdown. If you have not created your HTTP Linked Service, select **New**.

    ![](Linked_Image_Files/lab6_11.jpg)

1. In the New Linked Service (HTTP) screen, specify the url of the moviesDB csv file. You can access the data with no authentication required using the following endpoint:

    https://raw.githubusercontent.com/djpmsft/adf-ready-demo/master/moviesDB.csv

1. Place this in the **Base URL** text box. 

1. In the **Authentication type** drop down, select **Anonymous**. and click on **Create**.

    ![](Linked_Image_Files/lab6_12.jpg)

1. Once you have created and selected the linked service, specify the rest of your dataset settings. These settings specify how and where in your connection we want to pull the data. As the url is pointed at the file already, no relative endpoint is required. As the data has a header in the first row, set **First row as header** to be true and select Import schema from **connection/store** to pull the schema from the file itself. Select **Get** as the request method. You will see the followinf screen

    ![](Linked_Image_Files/lab6_13.jpg)
           
    - Click **OK** once completed.
   
    a. To verify your dataset is configured correctly, click **Preview Data** in the Source tab of the copy activity to get a small snapshot of your data.

    ![](Linked_Image_Files/lab6_14.jpg)

### Task 3: Create a new ADLS Gen2 dataset sink

1. Click on the **Sink tab**, and the click **+ New**

    ![](Linked_Image_Files/lab6_15.jpg)

1. Select the **Azure Data Lake Storage Gen2** tile and click **Continue**.

    ![](Linked_Image_Files/lab6_16.jpg)

1. Select the **DelimitedText** format tile and click **Continue**.

    ![](Linked_Image_Files/lab6_17.jpg)

1. In Set Properties blade, give your dataset an understandable name such as **ADLSG2** and click on the **Linked Service** dropdown. If you have not created your ADLS Linked Service, select **New**.

    ![](Linked_Image_Files/lab6_18.jpg)

1. In the New linked service (Azure Data Lake Storage Gen2) blade, select your authentication method as **Account key**, select your **Azure Subscription** and select your Storage account name of **awdlsstudxxxxxx**. You will see a screen as follows:

    ![](Linked_Image_Files/lab6_19.jpg)

1. Click on **Create**

1. Once you have configured your linked service, you enter the set properties blade. As you are writing to this dataset, you want to point the folder where you want moviesDB.csv copied to. In the example below, I am writing to folder so **output** (put this value in directory) in the **file system** as **data** (put this value in file system),refer below image, if have doubts. While the folder can be dynamically created, the file system must exist prior to writing to it. Set **First row as header** to be true. You can either Import schema from **sample file** (use the moviesDB.csv file from **C:\AllFiles\DP-200-Implementing-an-Azure-Data-Solution-master\Labfiles\Starter\DP-200.7\SampleFiles**)  

    ![](Linked_Image_Files/lab6_20_1.jpg)

1. Click **OK** once completed.

### Task 4: Test the Copy Activity

At this point, you have fully configured your copy activity. To test it out, click on the **Debug** button at the top of the pipeline canvas. This will start a pipeline debug run.

   ![](Linked_Image_Files/lab6_21.jpg)

1. To monitor the progress of a pipeline debug run, click on the **Output** tab of the pipeline

1. To view a more detailed description of the activity output, click on the eyeglasses icon. This will open up the copy monitoring screen which provides useful metrics such as Data read/written, throughput and in-depth duration statistics.

   ![](Linked_Image_Files/lab6_23_1.jpg)

1. To verify the copy worked as expected, open up your **awdlsstuddxxxxxx** storage account and select containers and open data and then open output folder and view the .txt file and you can see the values same as that from the movies.csv file. 

    ![](Linked_Image_Files/lab6_22.jpg)

## Exercise 3: Transforming Data with Mapping Data Flow
  
Estimated Time: 30 minutes

Individual exercise

Now that you have moved the data into Azure Data Lake Store Gen2, you are ready to build a Mapping Data Flow which will transform your data at scale via a spark cluster and then load it into a Data Warehouse. 
  
The main tasks for this exercise are as follows:

1. Preparing the environment

1. Adding a Data Source

1. Using Mapping Data Flow transformation

1. Writing to a Data Sink

1. Running the Pipeline

### Task 1: Preparing the environment

1. **Turn on Data Flow Debug** Turn the **Data Flow Debug** slider located at the top of the authoring module on. 

    > NOTE: Data Flow clusters take 5-7 minutes to warm up.

    ![](Linked_Image_Files/lab6_24.jpg)
    
    ![](Linked_Image_Files/lab6_25.jpg)
    
1. **Add a Data Flow activity** In the Activities pane, open the Move and Transform accordion and drag the **Data Flow** activity onto the pipeline canvas. In the blade that pops up, click **Create new Data Flow** and select **Data Flow** and then click **OK**. Click on the  **pipeline1** tab and drag the green box from your Copy activity to the Data Flow Activity to create an on success condition. You will see the following in the canvass:

    ![](Linked_Image_Files/lab6_26.jpg)
    
    ![](Linked_Image_Files/lab6_27.jpg)
    
    ![](Linked_Image_Files/lab6_26_1.jpg)

1. Now the pipeline should look like the below image.

    ![](Linked_Image_Files/lab6_27_2.jpg)

### Task 2: Adding a Data Source

1. Double-click on the dataflow tab to create a dataflow structure.

    ![](Linked_Image_Files/lab6_27_1.jpg)
1. Click on the **Add Source** button.

    ![](Linked_Image_Files/lab6_28.jpg)

1. **Add an ADLS source** Double click on the Mapping Data Flow object in the canvas. Click on the Add Source button in the Data Flow canvas. In the **Source dataset** dropdown, select your **ADLSG2** dataset used in your Copy activity

    ![Adding a Source to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/lab6_28_1.jpg)

1. If your dataset is pointing at a folder with other files, you may need to create another dataset or utilize parameterization to make sure only the moviesDB.csv file is read

1. If you have not imported your schema in your ADLS, but have already ingested your data, go to the dataset's 'Schema' tab and click 'Import schema' so that your data flow knows the schema projection.

1. Once your debug cluster is warmed up, verify your data is loaded correctly via the Data Preview tab. Once you click the refresh button, Mapping Data Flow will show calculate a snapshot of what your data looks like when it is at each transformation.
  
### Task 3: Using Mapping Data Flow transformation

1. Please read the instructions carefully and if any doubts, you can also refer the images.

1. **Add a Select transformation to rename and drop a column** In the preview of the data, you may have noticed that the "Rotton Tomatoes" column is misspelled. To correctly name it and drop the unused Rating column, you can add a [Select transformation](https://docs.microsoft.com/azure/data-factory/data-flow-select) by clicking on the + icon next to your ADLS source node and choosing Select under Schema modifier.
    
    ![Adding a Transformation to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/lab6_29.jpg)

    In the **Name as** field, change 'Rotton' to 'Rotten'. To drop the Rating column, hover over it and click on the trash can icon. (Scroll down to see the columns)

    ![Using the Select Transformation to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/lab6_30.jpg)

1. **Add a Filter Transformation to filter out unwanted years** Say you are only interested in movies made after 1951. You can add a [Filter transformation](https://docs.microsoft.com/azure/data-factory/data-flow-filter) to specify a filter condition by clicking on the **+ icon** next to your Select transformation and choosing **Filter** under Row Modifier. 

    ![](Linked_Image_Files/lab6_31.jpg)

1. Click on the **expression box** to open up the [Expression builder](https://docs.microsoft.com/azure/data-factory/concepts-data-flow-expression-builder) as shown in the image below and enter in your filter condition. Using the syntax of the [Mapping Data Flow expression language](https://docs.microsoft.com/azure/data-factory/data-flow-expression-functions),**toInteger(year) > 1950** (enter this value in **Filter On** Box) will convert the string year value to an integer and filter rows if that value is above 1950.

   ![](Linked_Image_Files/lab6_31_1.jpg)
   
   ![](Linked_Image_Files/lab6_31_2.jpg)

   ![](Linked_Image_Files/lab6_32.jpg)


1. **Add a Derive Transformation to calculate primary genre** As you may have noticed, the genres column is a string delimited by a '|' character. If you only care about the *first* genre in each column, you can derive a new column named **PrimaryGenre** via the [Derived Column](https://docs.microsoft.com/azure/data-factory/data-flow-derived-column) transformation by clicking on the **+ icon** next to your Filter transformation and choosing Derived under Schema Modifier. 

    ![](Linked_Image_Files/lab6_33.jpg)

1. Similar to the filter transformation, the derived column uses the Mapping Data Flow expression builder to specify the values of the new column.The value for the expression is **iif(locate("|",genres) > 1,left(genres, locate("|",genres)-1),genres)** (It will be better if you could type this expression).

    ![Using the Derived Transformation to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/lab6_34.jpg)

    In this scenario, you are trying to extract the first genre from the genres column which is formatted as 'genre1|genre2|...|genreN'. Use the **locate** function to get the first 1-based index of the '|' in the genres string. Using the **iif** function, if this index is greater than 1, the primary genre can be calculated via the **left** function which returns all characters in a string to the left of an index. Otherwise, the PrimaryGenre value is equal to the genres field. You can verify the output via the expression builder's Data preview pane.

1. **Rank movies via a Window Transformation** Say you are interested in how a movie ranks within its year for its specific genre. You can add a [Window transformation](https://docs.microsoft.com/azure/data-factory/data-flow-window) to define window-based aggregations by clicking on the **+ icon** next to your Derived Column transformation and clicking Window under Schema modifier.

    ![](Linked_Image_Files/lab6_35.jpg)

1. To accomplish this, specify what you are windowing over, what you are sorting by, what the range is, and how to calculate your new window columns. In this example, we will window over PrimaryGenre and year with an unbounded range, sort by Rotten Tomato descending, a calculate a new column called RatingsRank which is equal to the rank each movie has within its specific genre-year.(If need help please refer below images)

    ![Window Over](Linked_Image_Files/WindowOver.PNG "Window Over")

    ![Window Sort](Linked_Image_Files/WindowSort.PNG "Window Sort")

    ![Window Bound](Linked_Image_Files/WindowBound.PNG "Window Bound")

    ![Window Rank](Linked_Image_Files/WindowRank.PNG "Window Rank")

1. **Aggregate ratings with an Aggregate Transformation** Now that you have gathered and derived all your required data, we can add an [Aggregate transformation](https://docs.microsoft.com/azure/data-factory/data-flow-aggregate) to calculate metrics based on a desired group by clicking on the **+ icon** next to your Window transformation and clicking Aggregate under Schema modifier. 

    ![](Linked_Image_Files/lab6_36.jpg)
    
1. As you did in the window transformation, lets group movies by PrimaryGenre and year

    ![Using the Aggregate Transformation to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/M07-E03-T03-img10.png)

    In the Aggregates tab, you can aggregations calculated over the specified group by columns. For every genre and year, lets get the average Rotten Tomatoes rating, the highest and lowest rated movie (utilizing the windowing function) and the number of movies that are in each group. Aggregation significantly reduces the amount of rows in your transformation stream and only propagates the group by and aggregate columns specified in the transformation. Provide the following values as shown in the image.
    **Note:- while entering these names please enter the column names correctly and also check no spaces etc. are entered accidentally**
    * AverageRating - avg(toInteger({Rotten Tomato}))
    
        ![](Linked_Image_Files/lab6_37.jpg)
    Add the following columns also :-
    * HighestRated  - first(title)
    * LowestRated   - last(title)
    * NumberOfMovies - count()

    ![Configuring the Aggregate Transformation to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/M07-E03-T03-img11.png)

    * To see how the aggregate transformation changes your data, use the Data Preview tab
   

1. **Specify Upsert condition via an Alter Row Transformation** If you are writing to a tabular sink, you can specify insert, delete, update and upsert policies on rows using the [Alter Row transformation](https://docs.microsoft.com/azure/data-factory/data-flow-alter-row) by clicking on the + icon next to your Aggregate transformation and clicking Alter Row under Row modifier.

    ![](Linked_Image_Files/lab6_38.jpg)

1. Since you are always inserting and updating, you can specify that all rows will always be upserted. in alter row conditions select Upsert If and set to true()

    ![Using the Alter Row Transformation to a Mapping Data Flow in Azure Data Factory](Linked_Image_Files/lab6_39.jpg)
    
### Task 4: Create a SQL Data Warehouse database

1. Navigate to your windows virtual machine desktop, click on the **Search**, and type **"SQL Server"** and then click on **Microsoft SQL Server Management Studio 18**

1. In the **Connect to Server** dialog box, fill in the following details
    - Server Name: **dwhservice-deploymentID.database.windows.net** (navigate to resource group awrgstud-deploymentId and click on sql server dwhservice-deployment and from the overview copy the server name)
    - Authentication: **SQL Server Authentication**
    - Username: **sqladmin**
    - Password: **Pa55w.rd**

1. In the **Connect to Server** dialog box, click **Connect** 

1. In **SQL Server Management Studio**, in Object Explorer, right click **dwhservice-deploymentID.database.windows.net** and click on **New Query**. 

1. In the query window, create a DataWarehouse database named **DWDB**, with a service objective of DW100 and a maximum size of 1024GB. Click on **Execute**.

    ```SQL
    CREATE DATABASE DWDB COLLATE SQL_Latin1_General_CP1_CI_AS
    (
        EDITION             = 'DataWarehouse'
    ,   SERVICE_OBJECTIVE   = 'DW100C'
    ,   MAXSIZE             = 1024 GB
    );
    ```

    > **Note**: The creation of the database takes approximately 2 minutes.

1. Create a **master key** against the **DWDB** database. Expand dwhservice-deploymentID.database.windows.net in Object explorer , click databases and then right click on DWDB , select **NEW QUERY**. In the query editor, type in the following code and Click on **Execute**.

    > **Note:-** if a pop-up appears click **yes always**

    ```SQL
    CREATE MASTER KEY;
    ```

### Task 5: Writing to a Data Sink

1. Navigate back to data factory tab.

1. **Write to a Azure Synapse Analytics Sink** Now that you have finished all your transformation logic, you are ready to write to a Sink.
    1. Add a **Sink** by clicking on the **+ icon** next to your Upsert transformation and clicking Sink under Destination.
        ![](Linked_Image_Files/lab6_40.jpg)
    1. In the Sink tab, create a new data warehouse dataset via the **+ New button**.
        ![](Linked_Image_Files/lab6_41.jpg)
    1. Select **Azure Synapse Analytics** from the tile list.
        ![](Linked_Image_Files/lab6_42.jpg)
    1. Select a new linked service and configure your Azure Synapse Analytics connection to connect to the DWDB database created in the previous step. Click **Create** when finished.
    
        ![Creating an Azure Synapse Analytics connection in Azure Data Factory](Linked_Image_Files/M07-E03-T04-img01.png)
    
    1. In the dataset configuration, select **Create new table** and enter in the schema of **Dbo** and the  table name of **Ratings**. Click **OK** once completed.

        ![Creating an Azure Synapse Analytics table in Azure Data Factory](Linked_Image_Files/M07-E03-T04-img02.png)
    
    1. Since an upsert condition was specified, you need to go to the Settings tab and select 'Allow upsert' based on key columns PrimaryGenre and year.
    
        ![Configuring Sink settings in Azure Data Factory](Linked_Image_Files/M07-E03-T04-img03.png)
    
At this point, You have finished building your 8 transformation Mapping Data Flow. It's time to run the pipeline and see the results!

   ![Completed Mapping Data Flow in Azure Data Factory](Linked_Image_Files/M07-E03-T04-img04.png)

## Task 5: Running the Pipeline

1. Make sure you have data flow debug selected.

   ![](Linked_Image_Files/data-flow-debug.jpg)
    
1. Go to the pipeline1 tab in the canvas. Because Azure Synapse Analytics in Data Flow uses [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide?view=sql-server-2017), you must specify a blob or ADLS staging folder. In the Execute Data Flow activity's settings tab, open up the PolyBase accordion and select your ADLS linked service and specify a staging folder path.

    ![PolyBase configuration in Azure Data Factory](Linked_Image_Files/M07-E03-T05-img01.png)

1. Before you publish your pipeline, run another debug run to confirm it's working as expected. Looking at the Output tab, you can monitor the status of both activities as they are running.

1. Once both activities succeeded, you can click on the eyeglasses icon next to the Data Flow activity to get a more in depth look at the Data Flow run.

1. If you used the same logic described in this lab, your Data Flow should will written 737 rows to your SQL DW. You can go into [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) to verify the pipeline worked correctly and see what got written.

1. To check the values right click DWDB database and in new query enter the mentioned queries - **select count(*) as TotalCount From Dbo.Ratings** , **select * from Dbo.Ratings**

    ![Querying the results in SQL Server Management Studio](Linked_Image_Files/M07-E03-T05-img02.png)

## Exercise 4: Azure Data Factory and Databricks
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Generate a Databricks Access Token.

1. Generate a Databricks Notebook

1. Create Linked Services

1. Create a Pipeline that uses Databricks Notebook Activity.

1. Trigger a Pipeline Run.

### Task 1: Generate a Databricks Access Token.

1. In the Azure portal, click on **Resource groups** and then click on **awrgstudxx**, and then click on **xxxxxx** where xxxxxx is the deployment id.

1. Click on **Launch Workspace**

1. Click the user **profile icon** in the upper right corner of your Databricks workspace.

1. Click **User Settings**.

1. Go to the Access Tokens tab, and click the **Generate New Token** button.

1. Enter a description in the **comment** "For ADF Integration" and set the **lifetime** period of 10 days and click on **Generate**

1. Copy the generated token and store in Notepad, and then click on **Done**.

### Task 2: Generate a Databricks Notebook

1. Please ensure if the cluster is running. Click on **Clusters** from left navigation bar , select **awdbclstud** and click on start.

1. On the left of the screen, click on the **Workspace** icon, then click on the arrow next to the word Workspace, and click on **Create** and then click on **Folder**. Name the folder **adftutorial**, and click on **Create Folder**. The adftutorial folder appears in the Workspace.

1. Click on the drop down arrow next to adftutorial, and then click **Create**, and then click **Notebook**.

1. In the Create Notebook dialog box, type the name of **mynotebook**, and ensure that the language states **Python**, and then click on **Create**. The notebook with the title of mynotebook appears/

1. In the newly created notebook "mynotebook'" add the following code:

    ```Python
    # Creating widgets for leveraging parameters, and printing the parameters

    dbutils.widgets.text("input", "","")
    dbutils.widgets.get("input")
    y = getArgument("input")
    print ("Param -\'input':")
    print (y)
    ```

    > **Note** that the notebook path is **/adftutorial/mynotebook**

### Task 3: Create Linked Services

1. In Microsoft Edge, click on the tab for the portal In the Azure portal, and return to Azure Data Factory.

1. In the **data-factory-deploymentId** screen, click on **Author & Monitor**. Another tab opens up to author an Azure Data Factory solution.

1. On the left hand side of the screen, click on the **Manage** icon. This opens Connections section.

1. Under **Connections**, u can find linked services and then click on **+ New**.

1. In the **New Linked Service**, at the top of the screen, click on **Compute**, and then click on **Azure Databricks**, and then click on **Continue**.

1. In the **New Linked Service (Azure Databricks)** screen, fill in the following details and click on **Finish**
    - **Name**: dbls
    - **Databricks Workspace**: xxxxxx, where xxxxxx is the deployment id
    - **Select cluster**: Existing interactive cluster
    - **Domain/ Region**: should be populated
    - **Access Token**: Copy the access token from Notepad and paste into this field
    - **Choose from existing cluster**: awdbclstud
    - Leave other options to their default settings

    > **Note**: When you click on finish, you are returned to the **Author & Monitor** screen where the xx_dbls has been created, with the other linked services created in the previous exercize.

### Task 5: Create a pipeline that uses Databricks Notebook Activity.

1. On the left hand side of the screen, under Factory Resources, click on the **+** icon, and then click on **Pipeline**. This opens up a tab with a Pipeline designer.

1. At the bottom of the pipeline designer, click on the parameters tab, and then click on **+ New**

1. Create a parameter with the Name of **name**, with a type of **string**

1. Under the **Activities** menu, expand out **Databricks**.

1. Click and drag **Notebook** onto the canvas.

1. In the properties for the **Notebook1** window at the bottom, complete the following steps:
    - Switch to the **Azure Databricks** tab.
    - Select **dbls** which you created in the previous procedure.

    - Switch to the **Settings** tab, and put **/adftutorial/mynotebook** in Notebook path.
    - Expand **Base Parameters**, and then click on **+ New**
    - Create a parameter with the Name of **input**, with a value of **@pipeline().parameters.name**

1. In the **Notebook1**, click on **Validate**, next to the Save as template button. As window appears on the right of the screen that states "Your Pipeline has been validated.
No errors were found." Click on the >> to close the window.

1. Click on the **Publish All** to publish the linked service and pipeline.

    > **Note**: A message will appear to state that the deployment is successful.

### Task 6: Trigger a Pipeline Run

1. In the **Notebook1**, click on **Add trigger**, and click on **Trigger Now** next to the Debug  button.

1. The **Pipeline Run** dialog box asks for the name parameter. Use **/path/filename** as the parameter here. Click Finish. A red circle appear above the Notebook1 activity in the canvas.

### Task 7: Monitor the Pipeline

1. On the left of the screen, click on the **Monitor** tab. Confirm that you see a pipeline run. It takes approximately 5-8 minutes to create a Databricks job cluster, where the notebook is executed.

1. Select **Refresh** periodically to check the status of the pipeline run.

1. To see activity runs associated with the pipeline run, select **View Activity Runs** in the **Actions** column.

### Task 8: Verify the output

1. In Microsoft Edge, click on the tab **mynotebook - Databricks** 

1. In the **Azure Databricks** workspace, click on **Clusters** and you can see the Job status as pending execution, running, or terminated.

1. Click on the cluster **awdbclstud**, and then click on the **Event Log** to view the activities.
