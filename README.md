# PySparkTemplates
Some basic PySpark templates for parallel processing of data

## Parallisation
All dataframes are saves a dictionary with the following structure dataframe_dictionary = {<dataframe_name>{<version>;<dataframe>}}. This dictionary is interated over every code-block as as a loop. AS a result the operation is written as a function and executed using ThreatPoolExecutor. 

def function(source, configs, dataframe_collection):
  df = dataframe_collection[source]["unclean"]
  df_clean = clean_schema(dataframe_collection[source]["cleaned"])
  dataframe_collection[source]["cleaned"] = df clean

with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(process_source, source, configs, dataframe_collection) for source, configs in source_configs.items()]
    for future in as_completed(futures):
        future.result()

## API request

## Processing of JSON data
### Ingestion
### Exploding JSON
### Flattening JSON
### Standardizing schema and columns
### Saving as Parquet

## Processing of CSV data
### Ingestion
### Standardizing schema and columns
### Saving as Parquet
