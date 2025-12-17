## Task B: Transformation Logic & Business Rules Design

This section outlines the business rules applied during the transformation phase to resolve data quality issues found in the raw smart-meter data.

### 1. Unit Standardization
* **Problem:** Inconsistent measurement units; some meters report in Watts (W) while others use Kilowatts (kW).
* **Rule:** If `Energy_Unit` == "W", divide the `Reading_Value` by 1000 and update the unit to "kW".
* **Goal:** Ensure all energy data is stored in a standard unit (kW) for accurate aggregation.

### 2. Handling Missing Values
* **Problem:** Temporary Wi-Fi outages cause gaps in the time series (Null values).
* **Rule:** If `Energy_Reading` or `Timestamp` is **NULL**, flag the record as "Invalid" and exclude it from peak-usage calculations.
* **Goal:** Prevent incomplete data from skewing predictive analytics and reporting.

### 3. Faulty Meter Detection
* **Problem:** Need to detect abnormal or faulty smart meters automatically.
* **Rule:** If a meter reports a reading of **0** for a duration exceeding 24 hours, mark the `Meter_ID` as "Potential Fault".
* **Goal:** Proactive maintenance and identifying hardware failures.

### 4. Data Format Optimization
* **Problem:** Raw data arrives in CSV format, which is inefficient for large-scale historical analytics.
* **Rule:** Convert validated data from CSV to **Parquet** format before archiving.
* **Goal:** Optimize storage costs and query performance for long-term analysis.
