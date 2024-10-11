## Incident

Suddenly there is alert from the monitoring system that CPU usage is 100% and the application is not responding. But the database CPU still normal.

From the logs, there is spike in the number of requests and the application is not able to handle the load evenly. The number of request concentrated in to few features. 

## Impact

Here the list of features that are slow ranked by the number of requests:

1. Attaching files
2. Sending messages
3. Viewing messages

Those features are the main features of the app. The app is not able to handle the load and the app is not available.

## Immediate Action Taken

1. Increase the number of allocated CPU and memory for the server to twice the current capacity.

## Root Cause Analysis

After tracing down from performance monitoring tools from the endpoint with high latency, the slow features are caused by the following reasons:

1. Attaching files
    * The file is uploaded to the server and the server is processing the file. The file is not processed in parallel.

2. Sending and Delivering messages
    * Since the app is using monolithic architecture, endpoints related to sending messages are sharing same CPU and memory resources.

3. Not using queue mechanism
    * The app is not using queue mechanism to handle the load. The app is processing the request synchronously.

## Recommended Solution

Refactor the app into Service Oriented Architecture (SOA) and use queue mechanism to handle the load.

### Action Plan

1. Identify and break down available features into services.
2. Implement API gateway to route the request to the correct service.
3. Use queueing and async processing to handle the load.
    * Use RabbitMQ or Kafka to handle the request and avoid overloading the server.
4. Scalability
    * Apply autoscaling to the each independent service to handle the load.
5. Monitoring and Alerting
    * Setup monitoring tools like sentry, prometheus, grafana.
    * Setup tracing tools like jaeger or opentelemetry.
6. CI/CD Pipeline
    * Setup auto deployment.
    * Setup reproducible tests.

# Expected Outcome

1. The app is able to handle the load.
2. The app is available.
3. The app is able to scale horizontally.
