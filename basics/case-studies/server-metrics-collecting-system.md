# Metrics monitoring system

## Problem description
- There is roughly 1000 servers, how to define an interface to collect the metrics? What database to store these metrics, scalability, and fault tolerance, ...

## Functional requirements
- Data to be collected includes CPU usage, memory usage, disk usage, system logs, web server access, error logs.
- Users should be able to view real-time and historical data on a web-based dashboard.

## Summary
- Collect **system metrics** from **servers**
- Time series data -> **high write-throughput**
    - TimeScaleDB

## High-level overview
- Presentation layer (front-end) - client-side, dashboard
- Business logic layer (redirections)
- Service layer:
    - Stream processing service (data intake)
    - Storage service (database service to store metrics)
    - Query service (APIs for data retrieval)
    - Alerting service (subscribes to the storage service to alert on abnormal data reads)
- Data layer:
    - Relational database for storing metrics

## Database
- 

## Services
### Stream processing service - just for write
- POST /metrics
    - Input: json
    ```json
    {
        server_id: "...",
        timestamp: "...",
        metrics: {
            cpu_usage: 70.5,
            memory_usage: 10,
            disk_io: {
                read_iops: 120,
                write_iops: 100
            }
    }
    ```
- POST /logs
    - Input: json
    ```json
    {
        server_id: "...",
        timestamp: "...",
        message: "...",
        type: "..." // log, error
    }
    ```

### Query service - for read
- GET /metrics?server_id={server_id}&metric_type={metric_type}&start_time={start_time}&end_time={end_time}
- GET /logs?server_id={server_id}&log_type={log_type}&start_time={start_time}&end_time={end_time}

### Alert service

