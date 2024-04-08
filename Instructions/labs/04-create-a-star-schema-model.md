# Lab4 - Create a star schema model

## Lab scenario

In this lab, you will use Power BI Desktop to develop a data model over the Azure Synapse Adventure Works data warehouse. The data model will allow you to publish a semantic layer over the data warehouse.

## Lab objectives
  
In this lab, you will perform:

- Create a Power BI connection to an Azure Synapse Analytics SQL pool
- Develop model queries
- Organize the model diagram

## Estimated timing: 30 minutes

## Architecture Diagram

![](../images/lab4-archy.png)

## Exercise 1: Set up Power BI

### Task 1: In this task, you will set up Power BI.

1. To open Power BI Desktop, on the Desktop, select the **Power BI Desktop** shortcut.

1. Select **X** located at the top-right of the getting started window.

    ![](../images1/dp-lab4-1-1.png)

1. At the top-right corner of Power BI Desktop, if you're not already signed in, select **Sign In**. Use the lab credentials to complete the sign in process.

    ![](../images/dp500-create-a-star-schema-model-image3.png)
	
1. Enter the Lab username in the **Enter your email address** and click on **continue**

    ![](../images1/dp-lab4-(1).png)
	
1. If Prompted Select **work or school** account and click continue on Let's get you signed in page.

    ![](../images1/dp-lab4-2.png)

1. Complete the sign up process by providing username and password:

     * Email/Username: <inject key="AzureAdUserEmail"></inject>

     * Password: <inject key="AzureAdUserPassword"></inject>

1. You will be redirected to the Power BI sign-up page in Microsoft Edge. Select **contiune**.

   >**Note**: In a web browser, go to [https://powerbi.com](https://powerbi.com/) in case it is not opened.
   
	![](../images1/dp-lab4-3.png)
	
1. If prompted **Signin** with following Username and Password.

    * Email/Username: <inject key="AzureAdUserEmail"></inject>

    * Password: <inject key="AzureAdUserPassword"></inject>
	
1. If stay signed in window Pops-up, select **No**

1. Select your **Country/Region (1)** and enter a 10 digit **phone number (2)** and select **Get started (3)**.

    ![](../images1/dp-lab4-(4).png)

1. Select **Get started** once more. You will be redirected to Power BI.

    ![](../images1/dp-lab4-5.png)

1. At the top-right, select the profile icon, and then select **Start trial**.

    ![](../images1/dp-lab4-(6).png)

1. When prompted, select **Start trial**.

    ![](../images1/dp-lab4-7.png)

1. Do any remaining tasks to complete the trial setup.

    >**Tip**: The Power BI web browser experience is known as the **Power BI service**.
	
1. Select Workspaces and **Create a Workspace**.
    
    ![](../images1/dp-lab4-8.png)

1. Create a workspace named **DP500-<inject key="Deployment ID" enableCopy="false" />** and select **Apply**.

    >**Note**: The workspace name must be unique within the tenant. If you're getting an error, change the workspace name.

    ![](../images1/dp-lab4-9.png)

1. Navigate back to Power BI Desktop. If you see **Sign in** in the top right corner of the screen, sign-in again using the credentials provided on the Resources tab of the lab environment. If you are already signed in, proceed to the next step.

    <img width="80" alt="image" src="https://user-images.githubusercontent.com/77289548/166337862-538a1900-ec67-44d1-905f-d404c5b0a58a.png">

1. Go to Power BI Desktop and select **File** then **Options and settings** then **Options** then **Security** and under Authentication Browser check **Use my default web browser** and select **OK**. Close Power BI Desktop. Do not save your file.

   >**Note**: You will open Power BI Desktop again in the upcoming exercises.

### Task 2: Start the SQL pool

In this task, you will start the SQL pool.

1. In a Microsoft Edge, go to [https://portal.azure.com](https://portal.azure.com/).

1. Use the lab credentials to complete the sign in process.

1. In the Azure portal, in the **Search resources, services, and docs** text box at the top of the Azure portal page, Search and select **Azure Synapse Analytics**
 
1. Select your Synapse workspace.

    ![](../images1/dp-lab4-10.png)

1. Scroll down on the Synapse workspace page, locate and select the dedicated SQL pool.

    ![](../images1/dp-lab4-11.png)

1. Resume the SQL pool.

    ![](../images1/dp-lab4-12.png)

    >**Important**: The SQL pool is a costly resource. Please limit the use of this resource when working on this lab. The final task in this lab will instruct you to pause the resource.

### Task 3: Link your Power BI workspace to Azure Synapse Analytics

In this task you will link your existing Power BI workspace to your Azure Synapse Analytics workspace.

1. From the dedicated SQL pool in the Azure Portal, select **Open in Synapse Studio** from the ribbon.

    ![](../images1/dp-lab4-13.png)

1. On the home page of Azure Synapse Studio, select **Visualize** to link your Power BI workspace.

    ![](../images/dp-lab4-(14).png)

1. From the **Workspace name** dropdown, select the workspace you created in the previous task and select **Create**.

    ![](../images1/dp-lab4-15.png)

1. Navigate to **Manage (1)**, select **Publish all (2)** and then click on **Publish (3)** to ensure changes are published.

    ![](../images1/dp-lab4-(16).png)
    
    ![](../images1/dp-lab4-17.png)

## Exercise 2: Develop a data model

In this exercise, you will develop a DirectQuery model to support Power BI analysis and reporting of the data warehouse reseller sales subject.

### Task 1: Download a dataset file

In this task, you will download a Power BI data source file from Synapse Studio.

1. In the Synapse Studio, on the left, select the Develop hub.

    ![](../images1/dp-lab4-(18).png)

1. In the **Develop** pane, expand **Power BI**, then expand the workspace, and then select **Power BI datasets**. If not present, Click **Publish all** to publish Workspace and refresh the browser.

    ![](../images1/dp-lab4-19-1.png)

    >**Note**: If you don't see any data here, confirm that your dedicated SQL pool is running and that your Power BI workspace is linked to your Synapse workspace.

1. In the **Power BI Datasets** pane, select **New Power BI Dataset**.

    ![](../images1/dp-lab4-19.png)

1. In the left pane, at the bottom, select **Start**.
	
1. Select your SQL pool, **sqldb-<inject key="Deployment ID" enableCopy="false" />** **(1)**, and then select **Continue (2)**.

    ![](../images1/dp-lab4-20.png)

1. To download the .pbids file, select **Download**.

    ![](../images1/dp-lab4-(21).png)

    >**Note**: A .pbids file contains a connection to your SQL pool. It's a convenient way to start your project. When opened, it will create a new Power BI Desktop solution that already stores the connection details to your SQL pool.

1. When the .pbids file has downloaded, **open it**.

   >**Note**: When the file opens, it will prompt you to create queries using the connection. You will define those queries in the next task.

### Task 2: Create model queries

In this task, you will create five Power Query queries that will each load as a table to your model.

1. In Power BI Desktop, in the **SQL Server Database** window, at the left, select **Microsoft Account**.

	![](../images1/dp-lab4-22.png)
	
1. Select **Sign In**.

1. Sign in using the lab Azure credentials provided.

1. From the drop down please select the option  **workspace<inject key="DeploymentID" enableCopy="false"/>.sql.azuresynapse.net;sqldb<inject key="DeploymentID" enableCopy="false"/>** **(1)** as shown below and click Select **Connect (2)**.

   ![](../images1/dp-lab4-(23).png)
   
1. In the **Navigator** window, select (don't check) the **DimDate** table.

1. In the right pane, notice the preview result, which shows a subset of the table rows.

    ![](../images1/dp-lab4-24.png)
    
1. To create queries (which will become model tables), check the following seven tables:

	- DimDate

	- DimProduct
  
	- DimProductCategory
  
	- DimProductSubcategory

	- DimReseller

	- DimSalesTerritory

	- FactResellerSales

1. To apply transformations to the queries, at the bottom-right, select **Transform Data**.

    ![](../images1/dp-lab4-25.png)

    >**Note**: Transforming the data allows you to define what data will be available in your model.


1. In the **Connection Settings** window, select the **DirectQuery (1)** option and click **OK (2)**.

    ![](../images1/dp-lab4-26.png)

   >**Note**: This decision is important. DirectQuery is a storage mode. A model table that uses DirectQuery storage mode doesn't store data. So, when a Power BI report visual queries a DirectQuery table, Power BI sends a native query to the data source. This storage mode can be used for large data stores like Azure Synapse Analytics (because it could be impractical or uneconomic to import large data volumes) or when near real-time results are required.

1. In the **Power Query Editor** window, in the **Queries** pane (located at the left), notice there is one query for each table you checked.

    ![](../images1/dp-lab4-27.png)

    >**Note**: You will now revise the definition of each query. Each query will become a model table when it's applied to the model. You will now rename the queries, so they're described in more friendly and concise ways, and apply transformations to deliver the columns required by the known reporting requirements.

1. Select the **DimDate** query.

    ![](../images1/dp-lab4-28.png)


1. In the **Query Settings** pane (located at the right), to rename the query, in the **Name** box, replace the text with **Date**, and then press **Enter**.

    ![](../images1/dp-lab4-29.png)


1. To remove unnecessary columns, on the **Home** ribbon tab, from inside the **Manage Columns** group, select the **Choose Columns** icon.

    ![](../images1/dp-lab4-29-1.png)

1. In the **Choose Columns** window, to uncheck all checkboxes, uncheck the first checkbox.

    ![](../images1/dp500-(32).png)


1. Check the following five columns and select **OK**.

	- DateKey

	- FullDateAlternateKey

	- EnglishMonthName

	- FiscalQuarter

	- FiscalYear

	 ![](../images1/dp-lab4-30.png)

	>**Note**: This selection of columns determine what will be available in your model.


1. In the **Query Settings** pane, in the **Applied Steps** list, notice that a step was added to remove other columns.

    ![](../images1/dp-lab4-31.png)
     
    >**Note**: Power Query defines steps to achieve the desired structure and data. Each transformation is a step in the query logic.

1. To rename the **FullDateAlternateKey** column, double-click the **FullDateAlternateKey** column header.

1. Replace the text with **Date**, and then press **Enter**.

    ![](../images1/dp-lab4-32.png)

1. Notice that a new applied step is added to the query.

    ![](../images1/dp-lab4-33.png)

1. Rename the following columns:

	- **EnglishMonthName** as **Month**

	- **FiscalQuarter** as **Quarter**

	- **FiscalYear** as **Year**

1. To validate the query design, in the status bar (located along the bottom of the window), verify that the query has five columns.

     ![](../images/dp500-checkColumns.png)

      >**Important**: If the query design does not match, review the exercise steps to make any corrections.

      >**Note**: The design of the **Date** query is now complete.

1. In the **Applied Steps** pane, right-click the last step, and then select **View Native Query**.

    ![](../images1/dp-lab4-34.png)

1. In the **Native Query** window, review the SELECT statement that reflects the query design.

   >**Note**: This concept is important. A native query is what Power BI uses to query the data source. To ensure best performance, the database developer should ensure this query is optimized by creating appropriate indexes, etc.

1. To close the **Native Query** window, select **OK**.

1. Select the **DimProductCategory** table. 
    
1. Rename the query to **Product Details**.

1. On the home tab of the ribbon, in the Combine group, select **Merge Queries.** 

   >**Note**: We are merging queries to get the product details, category and subcategory. This will be used in the Product dimension.

1. Select the **DimProductSubcategory (1)** table from the drop-down and select the **ProductCategoryKey (2)** Column in each table. Select **OK (1)**.

    ![](../images1/dp-lab4-35.png)

    >**Note**: Use the default join for this merge, which is a left outer join.

1. Expand the **DimProductSubcategory (1)** column. Select the **ProductSubcategoryKey (2)** and the **EnglishProductSubcategoryName (3)** columns. De-select **Use original column name as prefix (4)** and select **OK (6)**.

    ![](../images1/dp-lab4-1(36).png)

    >**Note**: The Expand feature allows joining tables based on foreign key constraints in the source data. The design approach taken by this lab is to join snowflake dimension tables together to produce a denormalized representation of the data.

1. To remove unnecessary columns, on the **Home** ribbon tab, from inside the **Manage Columns** group, select the **Choose Columns** icon.

1. In the **Choose Columns** window, to uncheck all checkboxes, uncheck the first checkbox.

1. Check the following columns and click **ok**.

   - ProductSubcategoryKey
   
   - EnglishProductCategoryName

   - EnglishProductSubcategoryName

   >**Note**: You should now have three columns with 37 rows.
   
   >**Note**: This selection of columns determine what will be available in your model.
   
1.  Select the **DimProduct** query.

      ![](../images1/dp-lab4-37.png)

1. In the **Query Settings** pane (located at the right), to rename the query, in the **Name** box, replace the text with **Product**, and then press **Enter**.

    ![](../images1/dp500-30-lab4.png)
   
1. On the home tab of the ribbon, in the Combine group, select **Merge Queries.** 

1. Select the **Product Details (1)** table from the drop down and select the **ProductSubcategoryKey (2)** column in both the Product table and the Product details table1 and select **OK (3)**.

     ![](../images1/dp-lab4-39.png)

1. Expand the Product Details column and select the **EnglishProductSubcategoryName** and the **EnglishProductCategoryName** columns. 

    ![](../images/dp500-45.png)

1. Select **OK**.

1.  To filter the query, in the **FinishedGoodsFlag (1)** column header, open the dropdown menu, uncheck **FALSE (2)** and Select **OK (3)**.

     ![](../images1/dp-lab4-41.png)
     
1. To remove unnecessary columns, on the **Home** ribbon tab, from inside the **Manage Columns** group, select the **Choose Columns** icon.

1. In the **Choose Columns** window, to uncheck all checkboxes, uncheck the first checkbox.

1. Check the following columns and click **ok**.

	- ProductKey

	- EnglishProductName

	- Color

	- EnglishProductSubcategoryName

	- EnglishProductCategoryName

    >**Note**: This selection of columns determine what will be available in your model.

1. Rename the following columns:

	- **EnglishProductName** as **Product**

	- **Product Details.EnglishProductCategoryName** as **Category**

	- **Product Details.EnglishProductSubcategoryName** as **SubCategory**

1. In the **Applied Steps** pane, right-click the last step, and then select **View Native Query**.

1. In the **Native Query** window, review the SELECT statement that reflects the query design.

1. To close the **Native Query** window, select **OK**.

1. Verify that the query has five columns.

   >**Note**: The design of the **Product** query is now complete.

1. Select the **DimReseller** query.

1. Rename the query as **Reseller**.

1. To remove unnecessary columns, on the **Home** ribbon tab, from inside the **Manage Columns** group, select the **Choose Columns** icon.

1. In the **Choose Columns** window, to uncheck all checkboxes, uncheck the first checkbox.

1. Check the following columns and click **ok**.

	- ResellerKey

	- BusinessType

	- ResellerName

    >**Note**: This selection of columns determine what will be available in your model.

1. Rename the following columns:

	- **BusinessType** as **Business Type** (separate with a space)

	- **ResellerName** as **Reseller**

1. Verify that the query has three columns.

   >**Note**: The design of the **Reseller** query is now complete.

1. Select the **DimSalesTerritory** query.

    ![](../images/dp500-49.png)

1. Rename the query as **Territory**.

1. To remove unnecessary columns, on the **Home** ribbon tab, from inside the **Manage Columns** group, select the **Choose Columns** icon.

1. In the **Choose Columns** window, to uncheck all checkboxes, uncheck the first checkbox.

1. Check the following columns and click **ok**.

	- SalesTerritoryKey

	- SalesTerritoryRegion

	- SalesTerritoryCountry

	- SalesTerritoryGroup

    >**Note**: This selection of columns determine what will be available in your model.

1. Rename the following columns:

	- **SalesTerritoryRegion** as **Region**

	- **SalesTerritoryCountry** as **Country**

	- **SalesTerritoryGroup** as **Group**

1. Verify that the query has four columns.

   >**Note**: The design of the **Territory** query is now complete.

1. Select the **FactResellerSales** query.

1. Rename the query as **Sales**.

1. To remove unnecessary columns, on the **Home** ribbon tab, from inside the **Manage Columns** group, select the **Choose Columns** icon.

1. In the **Choose Columns** window, to uncheck all checkboxes, uncheck the first checkbox.

1. Check the following columns and click **ok**.

	- ResellerKey

	- ProductKey

	- OrderDateKey

	- SalesTerritoryKey

	- OrderQuantity

	- UnitPrice

	
    >**Note**: This selection of columns determine what will be available in your model.

1. Rename the following columns:

	- **OrderQuantity** as **Quantity**

	- **UnitPrice** as **Price**

1. To add a calculated column, on the **Add Column** ribbon tab, from inside the **General** group, select **Custom Column**.

    ![](../images1/dp-lab4-42.png)


1. In the **Custom Column** window, in the **New Column Name** box, replace the text with **Revenue**.

1. In the **Custom Column Formula** box, enter the following formula:

	```
	[Quantity] * [Price]
	```

1. Select **OK**.

1. To modify the column data type, in the **Revenue** column header, select **ABC123**, and then select **Decimal Number**.

    ![](../images1/dp-lab4-43.png)

1. Review the native query, noticing the **Revenue** column calculation logic.

1. Verify that the query has seven columns.

   >**Note**: The design of the **Sales** query is now complete.

1. Right-click on the **Product Details** table and de-select **Enable load**. This will disable the load of the Product Details table to the data model, and it will not appear in the report.

    ![](../images1/dp-lab4-44.png)

1. Repeat this step, de-selecting Enable load, for the **DimProductSubcategory** table.

1. To apply the queries, on the **Home** ribbon tab, from inside the **Close** group, select the **Close &amp; Apply** icon.

   ![](../images1/dp-lab4-56.png)
 
   >**Note**: Each query is applied to create a model table. Because the data connection is using DirectQuery storage mode, only the model structure is created. No data is imported. The model now consists of one table for each query.

1. In Power BI Desktop, when the queries have been applied, at the bottom-left corner in the status bar, notice that the model storage mode is DirectQuery.

    ![](../images/dp500-57.png)
	
    > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
    > - Click Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation tab.
    > - Hit the Validate button for the corresponding task.
    > - If you receive a success message, you can proceed to the next task. If not, carefully read the error message and retry the step, following the instructions in the lab guide.
    > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.
    
### Task 3: Organize the model diagram

In this task, you will organize the model diagram to easily understand the star schema design.

1. In Power BI Desktop, at the left, select **Model** view.

    ![](../images1/dp-lab4-45.png)

1. To resize the model diagram to fit to screen, at the bottom-right, select the **Fit to screen** icon.

    ![](../images1/dp-lab4-46.png)
	 
1. Drag the tables into position so that the **Sales** fact table is located at the middle of the diagram, and the remaining tables, which are dimension tables, are located around the fact table.

1. If any of the dimension tables aren't related to the fact table, use the following instructions to create a relationship:

	- Drag the dimension key column (for example, **ProductKey**) and drop it on the corresponding column of the **Sales** table.

	- In the **Create Relationship** window, select **OK**.


1. Review the final layout of the model diagram.

    ![](../images/dp500-60.png)

    >**Note**: The creation of the star schema model is now complete. There are many modelling configurations that could now be applied, like adding hierarchies, calculations, and setting properties like column visibility.

1. Optionally, to save the solution, at the top-left, select the disk icon.

1. In the **Save As** window, go to the **C:\LabFiles\DP-500-Azure-Data-Analyst\Allfiles\04\MySolution** folder.

1. In the **File name** box, enter **Sales Analysis**.
   
    ![](../images1/dp-lab4-61.png)

1. Select **Save**.

1. Close Power BI Desktop.

   > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
   > - Click Lab Validation tab located at the upper right corner of the lab guide section and navigate to the Lab Validation tab.
   > - Hit the Validate button for the corresponding task.
   > - If you receive a success message, you can proceed to the next task. If not, carefully read the error message and retry the step, following the instructions in the lab guide.
   > - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

### Task 4: Pause the SQL pool

In this task, you will stop the SQL pool.

1. In a web browser, go to [https://portal.azure.com](https://portal.azure.com/).

1. Go to the resource group and locate the SQL pool named **sqldb<inject key="DeploymentID" enableCopy="false"/>**.

1. Pause the SQL pool.

### Review
In this lab, you have completed:
- Create a Power BI connection to an Azure Synapse Analytics SQL pool
- Develop model queries
- Organize the model diagram

## You have successfully completed the lab
