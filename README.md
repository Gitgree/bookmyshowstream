🎬 Real-Time Event Streaming Pipeline — Azure Event Hubs, Stream Analytics & Synapse
📘 Project Overview

This project simulates a real-time event-driven architecture for a platform similar to BookMyShow.
It demonstrates how booking and payment events can be streamed through Azure Event Hubs, processed in real time using Azure Stream Analytics, and stored in Azure Synapse Analytics for downstream analysis and reporting.

🧩 Project Components
1. mock_bookings.py

This Python script simulates real-time booking events and publishes them to Azure Event Hub (bookingstopic).

Key Features:

Generates continuous booking data streams using the Faker library.

Includes customer details, event metadata, and seat-level pricing.

Sends new booking events every 5 seconds.

Demonstrates event-based ingestion into Event Hub.

2. mock_payments.py

This script produces mock payment events and sends them to another Azure Event Hub (paymentstopic).

Key Features:

Generates corresponding payment events for bookings.

Includes payment ID, method, status, and timestamps.

Uses the same time-based event loop for continuous data streaming.

Represents a separate event stream for payment systems.

3. stream_analytics_job_query.sql

This SQL query powers the Azure Stream Analytics job that processes both booking and payment events in real time.

What It Does:

Reads data streams from the two Event Hubs (bookings and payments).

Transforms nested JSON using GetArrayElements for seat-level expansion.

Categorizes events (Concert, Play, Movie → Music, Theater, Cinema).

Joins bookings and payments on order_id within a 2-minute window.

Writes the transformed and joined data into Azure Synapse output (bookings-synapse).

4. synapse_table_creation.sql

This script creates the target fact table in Azure Synapse Analytics for storing the transformed stream output.

Creates:

Schema: bookymyshow

Table: bookings_fact — contains detailed, joined booking and payment event data.

Columns Include:

Booking details: order ID, customer info, event metadata, seats, etc.

Payment details: payment ID, method, amount, status, etc.

Enriched metadata: event category, booking day of week, booking hour, timestamps.

⚙️ End-to-End Workflow

Data Generation

Run mock_bookings.py and mock_payments.py to continuously publish events to two Azure Event Hubs.

Stream Processing

The Azure Stream Analytics job consumes both event streams.

Real-time transformation and joining logic are executed using stream_analytics_job_query.sql.

Data Storage

Processed data is written to Azure Synapse Analytics using the defined schema in synapse_table_creation.sql.

Analytics

You can query the final table (bookymyshow.bookings_fact) in Synapse to generate dashboards and reports.

🧠 Learning Objectives

Understand real-time data streaming with Azure Event Hubs.

Implement event-driven architecture for continuous data ingestion.

Use Azure Stream Analytics to transform and enrich streaming data.

Store and analyze streaming data in Azure Synapse Analytics.

🗂️ Folder Structure
├── mock_bookings.py                # Generates real-time booking events
├── mock_payments.py                # Generates real-time payment events
├── stream_analytics_job_query.sql  # Stream Analytics transformation & join logic
├── synapse_table_creation.sql      # Synapse schema and fact table creation
├── README.md                       # Project documentation

🚀 Future Enhancements

Add Power BI for real-time visualizations.

Introduce Azure Data Factory for historical batch data loading.

Implement event reprocessing and dead-letter handling.

Extend with serverless functions for event enrichment.
