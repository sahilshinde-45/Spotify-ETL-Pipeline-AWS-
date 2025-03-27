# Spotify-ETL-Pipeline-AWS
This architecture showcases the end-to-end Extract, Transform, Load (ETL) process for Spotify data analytics using AWS services. Below is the step-by-step breakdown of each component:

## 🛠️ Technologies Used

| Service        | Purpose |
|----------------|---------|
| **Amazon S3**      | Storage for raw and transformed data |
| **AWS Glue ETL**   | Serverless transformation of raw Spotify data |
| **AWS Glue Crawler** | Scans S3 data and creates table schemas in the Data Catalog |
| **AWS Athena**     | Serverless SQL querying of data directly from S3 |
| **Amazon QuickSight** | Visualization and business intelligence dashboards |

---

## 🧱 Architecture Diagram

![Architecture-diagram](https://github.com/user-attachments/assets/fb868a70-5669-4298-b782-36998e1f452c)

---

## 🚀 Getting Started

1. Upload raw data to S3 staging
2. Run the Glue ETL job
3. Trigger the Glue Crawler
4. Run Athena queries
5. Build dashboards in QuickSight

---

### 🔁 Pipeline Flow:

1. **S3 Staging**: Raw Spotify data is ingested and stored in an S3 bucket.

    <img width="1396" alt="S3-objectStorage" src="https://github.com/user-attachments/assets/0d9a5a9b-c1a9-44a1-b046-2de800b2bc4f" />

3. **Glue ETL**: Transforms and cleans the data, storing the output into a separate S3 bucket (DW).

    <img width="666" alt="Glue-ETL " src="https://github.com/user-attachments/assets/f1969111-164a-4a8e-9045-30641e9d4084" />
    
5. **S3 Data Warehouse**: Acts as a storage layer for processed, query-optimized data (e.g., Parquet).

    <img width="1126" alt="Transformed-data" src="https://github.com/user-attachments/assets/688063c6-c621-496d-ab20-3de36946d959" />

7. **Glue Crawler**: Scans the DW S3 bucket to detect schema and update the AWS Glue Data Catalog.

    <img width="1138" alt="Glue-Crawler" src="https://github.com/user-attachments/assets/27e776e7-87ee-4cf2-97c8-63352c7e47f2" />

9. **Athena**: Allows querying of data using SQL via the metadata registered by the crawler.
10. **QuickSight**: Connects to Athena to generate dynamic visual dashboards.

---

## 📊 Sample Athena Queries

### 🔹 Top 10 Artists by Popularity

```sql
SELECT 
    artist_name,
    COUNT(DISTINCT track_id) AS total_tracks,
    ROUND(AVG(popularity), 2) AS avg_popularity,
    ROUND(AVG(danceability), 2) AS avg_danceability,
    ROUND(AVG(energy), 2) AS avg_energy
FROM 
    spotify_data_table
GROUP BY 
    artist_name
ORDER BY 
    avg_popularity DESC
LIMIT 10;
```
### 🔹 Year-wise Trend Analysis

```sql
SELECT 
    year,
    COUNT(DISTINCT track_id) AS total_tracks,
    ROUND(AVG(popularity), 2) AS avg_popularity,
    ROUND(AVG(danceability), 2) AS avg_danceability,
    ROUND(AVG(energy), 2) AS avg_energy
FROM 
    spotify_data_table
WHERE 
    year IS NOT NULL
GROUP BY 
    year
ORDER BY 
    year ASC;
```




