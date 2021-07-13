# eCommerce_SnowFlake_DM


This project is a Snowflake version of the eCommerce Data Mart, I was tasked to create a Snowflake Schema data mart for an eCommerce sales company.
The company's OLTP system is in SQL Server and it contained 14 tables.

![eCommerce_OLTP](https://user-images.githubusercontent.com/82042663/125300500-b401a580-e2ef-11eb-8722-884c3ca4f4cd.PNG)


Similarly to the Star schema model Data Mart, I created a staging database, then created a Stored Procedure in SQL Server which joins all the tables
and stores them in a Temporary table. Then, I created a SSIS package and used Execute SQL Task to execute the stored Procedure
to create the temp table which served as a source in the Data Flow Task to load data into the staging table in the 
staging database.

![usp_Denorm_eCommerce](https://user-images.githubusercontent.com/82042663/125460985-49d13527-9c8f-4c18-80ec-00d4f55a8580.PNG)


![SSIS_eCommerce Staging](https://user-images.githubusercontent.com/82042663/125460407-3844780d-e2e4-4f2a-a1e2-2c8c4c1a4417.PNG)



I created a Data Mart and schemas Dim and Fact in SQL Server and the Data Mart contained the following Dimension 
and Fact tables:-

1. Dim.Cusotmers
2. Dim.Products
3. Dim.Shipments
4. Dim.Payment_Methods
5. Dim.Date
6. Fact.Invoice
7. Fact.Orders

![SnowFlake](https://user-images.githubusercontent.com/82042663/125461549-a0e58b33-2934-4751-9bf4-74fc416e5fb7.PNG)


I created another SSIS package to load the Dimension and Fact tables using the staging database table created earlier after applying transformations 
in the Data Flow task.

![SSIS_LoadDim_Facts](https://user-images.githubusercontent.com/82042663/125462353-0c045ce4-414b-43d2-af27-fe4300cc08e6.PNG)



In order to perform incremental load after initial load on the customers and product dimension![Update_Dim_Products](https://user-images.githubusercontent.com/82042663/125463435-f30513e5-1cfe-45c0-ac26-813f69b59b6c.PNG)
 tables, I used Lookup transformation and
OLE DB Command. Even though, it i obvious OLE DB Command is slow, because it performs row by row operation, it is used for now at least the 
source data is is not large so we will not have performance issues. I recommend to use other methods of incremental load when the data grows
in the future.

![update_Dim_Customers](https://user-images.githubusercontent.com/82042663/125463352-e60522fd-eecc-43cd-bd26-8ef483326b90.PNG)


![Uploading Update_Dim_Products.PNG…]()




After creating the packge to load all the Dimensions and the Fact tables, I created another Master package which executes first the staging Package and then
the package that loads the Dimension and Fact tables using Execute Package Task in the control flow.


![Master_Package](https://user-images.githubusercontent.com/82042663/125463830-081b4ec4-b410-441b-b682-c5939dcac2df.PNG)


Thank you for taking the time to take a look at this project.

Any feedback is much appreciated.

- Nebiyu Sahlu


