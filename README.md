# AzureProjectWithCICD

### HERE WE FIND THE SCRIPTS USED TO PERFORM ETL

1. we create a resources group in Azure
2. we create an azure storage account
3. we create an Azure Data Factory session
4. we create an Access Databricks connector
5. we set Azure Databricks Service
6. we create 4 containers in Azure storage account:
    - source: ingestion of all .csv files (nocs, athletes, coaches, events) from url. The ingestion is made by using Azure Data Factory HTTP linked service as source of ingestion and Azure Data Lake Storage Gen2 as sink dataset that corresponds to the bronze container.
    - bronze: no transformation but conversion of all .csv to .parquet so save resources.
    - silver: - no transformation for coaches and events thus we perform a parametric automated extraction with a pyspark notebook from bronze to silver by using a job (with a lookup task to extract the file paths from a json file and a for loop task to apply the         extraction/upload script for each path) and we convert the files format to .delta - specific complex transformation for athletes thus we use a specific non parametric pyspark script to extract athletes.parquet from bronze, apply all the transformations, and then load athletes.delta to silver. - specific transformation for nocs thus we apply the same logic used for athletes with a separate notebook
