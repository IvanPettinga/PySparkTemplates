# PySparkTemplates
Some basic PySpark templates for parallel processing of data

## Configuration
All dataframes have a config dictionary with their specific parameters. This can also be saved a JSON and imported or even stored in a database to collect your data parameters.

```
dataframe_configs = {
    "src_directory": "test",
    "explode_cols": ["test.data"],
    "flatten_cols": ["data"],
    "id_cols": ["primary_key"], #is gelijk aan UUID van zaak
    "primary_col_name": "primary_key",
    "sink_directory": "test",
    "included": pipeline_parameter,
    }

All configs are collected in a single dicitonary 
configs = {
    "test": test_configs,
```

## Parallisation
This dictionary is interated over every code-block as as a loop. As a result the operation is written as a function and executed using ThreatPoolExecutor. 

```
def function(source, configs, dataframe_collection):
  df = dataframe_collection[source]["unclean"]
  df_clean = clean_schema(dataframe_collection[source]["cleaned"])
  dataframe_collection[source]["cleaned"] = df clean
```
```
with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(process_source, source, configs, dataframe_collection) for source, configs in configs.items()]
    for future in as_completed(futures):
        future.result()
```

## API request

## Processing of JSON data
### Ingestion
```
def load_directory(source, configs, dataframe_collection):
    src_path = ADLS_PATH_SRC + "/" + configs["src_directory"]
    df_comp = spark.read.format("json").load(src_path)
    dataframe_collection[source] = {"comp": df_comp}
    print(f'Successfully loaded data from {configs["src_directory"]}')

# Set up parallel execution
with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(load_directory, source, configs, dataframe_collection) for source, configs in source_configs.items()]
    for future in as_completed(futures):
        future.result()
```

### Exploding JSON
### Flattening JSON
### Standardizing schema and columns
### Saving as Parquet

## Processing of CSV data
### Ingestion
### Standardizing schema and columns
### Saving as Parquet
