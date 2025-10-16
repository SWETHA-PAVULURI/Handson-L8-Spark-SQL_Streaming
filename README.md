# Real-Time Ride-Sharing Analytics with Apache Spark

This project implements a real-time analytics pipeline for a ride-sharing platform using Apache Spark Structured Streaming. It processes simulated live ride data, performs continuous aggregations, and analyzes fare trends over time using window-based streaming analytics.

---

## 📁 Project Structure

ride-sharing-analytics/
  ├── data_generator.py              # Python script to simulate live ride-sharing data
  ├── task1_streaming_ingestion.py   # Task 1: Ingest and parse streaming data
  ├── task2_driver_aggregations.py   # Task 2: Real-time driver-level aggregations
  ├── task3_windowed_analytics.py    # Task 3: Time-windowed fare trend analysis
  ├── output/                        # Output directory for CSV results
  ├── checkpoints/                   # Checkpoint directory for stateful operations
  └── README.md                      # Project documentation

---

## 🧪 Data Format
Each generated record is a JSON string representing one trip:

{
  "trip_id": "t123",
  "driver_id": "d456",
  "distance_km": 12.5,
  "fare_amount": 25.0,
  "timestamp": "2025-04-01T17:45:00"
}

---

## ▶️ How to Run

Step 1: Install Dependencies
  - pip install pyspark faker

Step 2: Start the Data Generator
  - Run in one terminal:
      python data_generator.py
  - Streams data continuously to localhost:9999

Step 3: Run Spark Streaming Tasks
  - Ensure Apache Spark is installed and spark-submit is available.

Task 1: Streaming Ingestion and Parsing
  - Command:
      spark-submit task1_streaming_ingestion.py
  - Reads and parses live data stream from the socket.
  - Prints structured results to the console.

Task 2: Real-Time Driver Aggregations
  - Command:
      spark-submit task2_driver_aggregations.py
  - Groups data by driver_id and computes:
      • Total fare per driver (SUM(fare_amount))
      • Average distance per driver (AVG(distance_km))
  - Writes results to:
      output/driver_aggregations/

Task 3: Windowed Time-Based Fare Analysis
  - Command:
      spark-submit task3_windowed_analytics.py
  - Converts timestamps to Spark TimestampType.
  - Performs aggregations over 5-minute windows sliding every 1 minute.
  - Writes results to:
      output/windowed_analytics/

---

## 📝 Tasks Overview

Task 1: Ingestion and Parsing
  - Reads streaming JSON data from a socket.
  - Parses records into structured Spark DataFrame columns.
  - Outputs results to the console for validation.

Task 2: Real-Time Aggregations
  - Groups data by driver_id.
  - Computes total fare and average distance per driver.
  - Writes each micro-batch result to CSV.

Task 3: Time-Windowed Analysis
  - Converts timestamp strings to TimestampType.
  - Aggregates fare_amount over 5-minute sliding windows.
  - Writes results to CSV files.

---

## 📦 Output Example (CSV)

"[2025-04-01 17:40:00,2025-04-01 17:45:00]", 210.0

Explanation:
  - The first column represents the time window range.
  - The second column is the total fare within that window.

---

## ✅ Requirements
  - Python 3.8+
  - Apache Spark 3.x
  - Dependencies:
      pip install pyspark faker

---

## 📌 Notes
  - Run the data generator and each Spark task in separate terminals.
  - Ensure output/ and checkpoints/ directories are writable.
  - Socket source is for local testing only (not production).

---

## 📚 References
  - Apache Spark Structured Streaming Documentation:
    https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html
