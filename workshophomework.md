Question 1: dlt Version
 !pip install dlt[duckdb]
 !dlt --version

 Question 2: Define & Run the Pipeline (NYC Taxi API)
Use dlt to extract all pages of data from the API.

Steps:

1️⃣ Use the @dlt.resource decorator to define the API source.

2️⃣ Implement automatic pagination using dlt's built-in REST client.

3️⃣ Load the extracted data into DuckDB for querying.

import dlt
from dlt.sources.helpers.rest_client import RESTClient
from dlt.sources.helpers.rest_client.paginators import PageNumberPaginator

@dlt.resource(name="rides") 
def paginated_getter():
  client = RESTClient(
      base_url="https://us-central1-dlthub-analytics.cloudfunctions.net/data_engineering_zoomcamp_api",
      paginator=PageNumberPaginator(
        base_page=1,
        total_path=None
    )
  )

  for page in client.paginate("data_engineering_zoomcamp_api"):
    yield page

# Call the function and assign the result to ny_taxi_data
ny_taxi_data = paginated_getter()


pipeline = dlt.pipeline(
    pipeline_name="ny_taxi_pipeline",
    destination="duckdb",
    dataset_name="ny_taxi_data"
)

load_info = pipeline.run(ny_taxi_data)
print(load_info)

import duckdb
from google.colab import data_table
data_table.enable_dataframe_formatter()

# A database '<pipeline_name>.duckdb' was created in working directory so just connect to it

# Connect to the DuckDB database
conn = duckdb.connect(f"{pipeline.pipeline_name}.duckdb")

# Set search path to the dataset
conn.sql(f"SET search_path = '{pipeline.dataset_name}'")

# Describe the dataset
conn.sql("DESCRIBE").df()

4 tables were created

Question 3. The total number of records extracted?

df = pipeline.dataset(dataset_type="default").rides.df()
df

10000


Question 4. Average trip duration

with pipeline.sql_client() as client:
    res = client.execute_sql(
            """
            SELECT
            AVG(date_diff('minute', trip_pickup_date_time, trip_dropoff_date_time))
            FROM rides;
            """
        )
    # Prints column values of the first row
    print(res)
[(12.3049,)]
