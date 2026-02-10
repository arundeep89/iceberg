Reference:
- https://github.com/abeltavares/real-time-data-pipeline (using rest api catalog)
- https://www.dremio.com/blog/using-flink-with-apache-iceberg-and-nessie/ (using nessie catalog, java flink job)


### Access the Services**

| **Service** | **URL** | **Credentials** |
| --- | --- | --- |
| **Kafka Control Center** | `http://localhost:9021` | *No Auth* |
| **Flink Dashboard** | `http://localhost:18081` | *No Auth* |
| **MinIO Console** | `http://localhost:9001` | `admin` / `password` |
| **Trino UI** | `http://localhost:8080/ui` | *No Auth* |
| **Superset** | `http://localhost:8088` | `admin` / `admin` |


**🔍 Query Data with Trino**
----------------------------

 **1\. Run Trino CLI**

```bash
docker-compose exec trino trino
```

**2\. Connect to Iceberg Catalog**

```sql
USE iceberg.db;
```

**3\. Query Processed Data**

```sql
SELECT * FROM iceberg.db.clickstream_sink
WHERE purchase_amount > 100
LIMIT 10;
```

📊 **Data Visualization with Apache Superset**
----------------------------------------------
1.  **Connect Superset to Trino:**

-   **SQLAlchemy URI:**

    ```bash
    trino://trino@trino:8080/iceberg/db
    ```
-   **Configure in Superset:**

    1.  Open `http://localhost:8088`
    2.  Go to **Data** → **Databases** → **+**
    3.  Use the above SQLAlchemy URI.

2.  **Create Dashboards:**