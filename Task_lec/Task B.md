## Task B: Transformation Logic & Business Rules Design

[cite_start]This section outlines the business rules applied during the transformation phase to resolve data quality issues found in the raw smart-meter data[cite: 10, 38].

### 1. Unit Standardization
* [cite_start]**Problem:** Inconsistent measurement units; some meters report in Watts (W) while others use Kilowatts (kW)[cite: 11, 12, 13].
* [cite_start]**Rule:** If `Energy_Unit` == "W", divide the `Reading_Value` by 1000 and update the unit to "kW"[cite: 40, 45].
* **Goal:** Ensure all energy data is stored in a standard unit (kW) for accurate aggregation.

### 2. Handling Missing Values
* [cite_start]**Problem:** Temporary Wi-Fi outages cause gaps in the time series (Null values)[cite: 14, 15].
* [cite_start]**Rule:** If `Energy_Reading` or `Timestamp` is **NULL**, flag the record as "Invalid" and exclude it from peak-usage calculations[cite: 41, 46].
* **Goal:** Prevent incomplete data from skewing predictive analytics and reporting.

### 3. Faulty Meter Detection
* [cite_start]**Problem:** Need to detect abnormal or faulty smart meters automatically[cite: 6].
* [cite_start]**Rule:** If a meter reports a reading of **0** for a duration exceeding 24 hours, mark the `Meter_ID` as "Potential Fault"[cite: 43, 47].
* **Goal:** Proactive maintenance and identifying hardware failures.

### 4. Data Format Optimization
* [cite_start]**Problem:** Raw data arrives in CSV format, which is inefficient for large-scale historical analytics[cite: 16, 17].
* [cite_start]**Rule:** Convert validated data from CSV to **Parquet** format before archiving[cite: 22, 55].
* **Goal:** Optimize storage costs and query performance for long-term analysis.
