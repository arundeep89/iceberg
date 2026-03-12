### Commands:
- cd duckdb_iceberg
- source .venv/bin/activate
- duckdb my_database.duckdb
- CREATE table flights as select * from read_csv_auto('./_resource/flights.csv');
- show tables;
- SELECT * FROM duckdb_tables();
- .exit
