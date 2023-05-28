# D365-WHS-Work-Template-Query-Import

## Classes
 1. DOWN01RunnableClass_WHSReplenishmentTemplateTransform
 2. DOWN01RunnableClass_WHSWorkTemplateQueryImport.xml

### WHS Replenishment Template Transform
Sometimes it is a real struggel to import your replenishment templates in D365 F&O with the right product or product variants queries. So that runnable class retrievs the description of the WHS replenishment template line and based on the description it creates the appropiate query.
The structure of the description should be only the product/itemid or product/itemid + "|" + sizeid. Example: 120000000 or 12000000|R0100

### WHSWorkTemplateQueryImport
With that class you can import work template queries into your production system that have been export from another sandbox system. To export the product queries you need to access the D365 F&O sandbox database (and do not forget to add your ip address to the firewall). There you can export the queries with a simple SQL query: 
  ```
    SELECT WorkTemplateCode, WorkTransType, CONVERT(VARCHAR(MAX), WorkTemplateQuery, 1) as 'WorkTemplateQuery' FROM WHSWorkTemplateTable
  ```
You need to save the results (with the header) into a CSV file and the column seperator must be a semi-colon ````;````
The you can import with running the class the csv file or you first modify your csv file and then import it with the runnable class from the browser.
Do not forget that the first line the csv file is going to be ignored as I assume that it should be the header column.
