## Task C: Single Record Lifecycle Explanation

A step-by-step breakdown of how a single smart-meter record is processed from upload to archival.

**Scenario:** A meter uploads a record: `{ID: 101, Val: 500, Unit: "W", Time: "10:00 AM"}`.

### Step 1: Ingestion (Upload to Raw Storage)
The smart meter sends the data file (CSV) to the cloud. It lands in the **Raw Data Storage** bucket. At this stage, the data is still "dark data" and unrefined.

### Step 2: Triggering Transformation
The arrival of the new file automatically acts as an event trigger, launching the serverless transformation process (ETL Pipeline) without manual intervention.

### Step 3: Cleaning & Validation
The system parses the record and applies the business rules defined in Task B:
* **Unit Check:** Detects "W", divides 500 by 1000 to get **0.5 kW**.
* **Null Check:** Confirms fields are not empty.
* **Fault Check:** Confirms the value is not an abnormal zero trend.

### Step 4: Structured Storage (Hot Path)
The cleaned record (`0.5 kW`) is written to the **Structured Database (RDS)**. This allows the operational team to query the data immediately for validation and monitoring.

### Step 5: Archival (Cold Path)
Simultaneously, the record is converted into **Parquet format** and stored in the **Data Lake Archive**. This ensures the data is optimized for future predictive analytics.

### Step 6: Completion & Error Handling
* **Success:** The pipeline logs the transaction as successful.
* **Failure:** If any step fails (e.g., database timeout), the system automatically retries or sends the record to a "Dead Letter Queue" for inspection.
