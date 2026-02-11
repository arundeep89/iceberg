Reference:
- https://github.com/abeltavares/real-time-data-pipeline (using rest api catalog)
- https://www.dremio.com/blog/using-flink-with-apache-iceberg-and-nessie/ (using nessie catalog, java flink job)


**📖 Overview**
---------------

This project demonstrates a **real-time end-to-end (E2E) data pipeline** designed to handle clickstream data. It shows how to ingest, process, store, query, and visualize streaming data using open-source tools, all containerized with Docker for easy deployment.

🔎 **Technologies Used:**

-   **Data Ingestion:** [Apache Kafka](https://kafka.apache.org/)  
-   **Stream Processing:** [Apache Flink](https://flink.apache.org/)  
-   **Object Storage:** [MinIO (S3-compatible)](https://min.io/)
-   **Data Lake Table Format:** [Apache Iceberg](https://iceberg.apache.org/)  
-   **Query Engine:** [Trino](https://trino.io/)  
-   **Visualization:** [Apache Superset](https://superset.apache.org/)    


**🔧 Setup Instructions**
-------------------------
### Start All Services

```bash
docker compose up -d
or
docker compose -f docker-compose-kraft.yml up -d
```

⚠️ **Note:** All components (Kafka, Flink, Iceberg, Trino, MinIO, and Superset) are containerized using Docker for easy deployment and scalabilit


### Access the Services

| **Service** | **URL** | **Credentials** |
| --- | --- | --- |
| **Kafka Control Center/UI** | `http://localhost:9021` | *No Auth* |
| **Flink Dashboard** | `http://localhost:18081` | *No Auth* |
| **MinIO Console** | `http://localhost:9001` | `admin` / `password` |
| **Trino UI** | `http://localhost:8080/ui` | `admin` |
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