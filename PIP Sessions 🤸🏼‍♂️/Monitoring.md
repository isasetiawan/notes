Monitoring is a practice gathering metrics and logs from the application and infrastructure to understand the performance and health of the system. Monitoring is essential for the following reasons:
- **Performance**: Monitoring helps to understand the performance of the application and infrastructure. It helps to identify the bottlenecks and optimize the system.
- **Health**: Monitoring helps to understand the health of the system. It helps to identify the issues before they become critical.
- **Cost**: Monitoring helps to understand the cost of the system. It helps to optimize the cost of the system.
Monitoring is focused on the following areas:
1. **Defined Metrics**: Monitoring should be focused on the metrics that are defined and agreed upon. It helps to understand the performance and health of the system.
2. **Alerting**: Monitoring should have alerting capabilities to notify the team when there are issues. It helps to identify the issues before they become critical.
3. **Dashboard**: Monitoring should have a dashboard to visualize the metrics. It helps to understand the performance and health of the system.

Monitoring could be separated into two levels, which are:
## Hardware Level
In ECS-like environment, some metric that should be monitored are:
1. **CPU**: Monitoring the CPU usage helps to understand the load on the system. It helps to identify the bottlenecks and optimize the system.
	1. ~~**Overall CPU Usage**: Monitoring the overall CPU usage helps to understand the load on the system.~~
	2. **Per Task CPU Usage**: Monitoring the CPU usage per task helps to understand the load on the system.
2. **Memory**: Monitoring the memory usage helps to understand the memory consumption of the system. It helps to identify the bottlenecks and optimize the system.
	1. ~~**Overall Memory Usage**: Monitoring the overall memory usage helps to understand the memory consumption of the system.~~
	2. **Per Task Memory Usage**: Monitoring the memory usage per task helps to understand the memory consumption of the system.
3. **Disk**: Monitoring the disk usage helps to understand the disk consumption of the system. It helps to identify the bottlenecks and optimize the system.
	1. **Disk I/O**: Monitoring the disk I/O helps to understand the disk consumption of the system.
	2. **Disk Space Usage**: Monitoring the disk space usage helps to understand the disk consumption of the system.
4. **Network**: Monitoring the network usage helps to understand the network consumption of the system. It helps to identify the bottlenecks and optimize the system.
	1. **Network I/O**: Monitoring the network I/O helps to understand the network consumption of the system.
	2. **Network Latency**: Monitoring the network latency helps to understand the network consumption of the system.
## Application Level
In application level, some metric that should be monitored are:
1. **Application Performance**: Monitoring the application performance helps to understand the performance of the application. It helps to identify the bottlenecks and optimize the application.
	1. **Response Time**: Monitoring the response time helps to understand the performance of the application.
	2. **Throughput**: Monitoring the throughput helps to understand the performance of the application.
2. **Application Logs**: Monitoring the application logs helps to understand the health of the application. It helps to identify the issues before they become critical.
3. **Container Lifecycle**: Monitoring the container lifecycle helps to understand the health of the container. It helps to identify the issues before they become critical. Some events that should be monitored is when the container is starting, running, stopping, and restarting.
4. **Dependency Monitoring**: Monitoring the dependencies helps to understand the health of the application. It helps to identify the issues before they become critical.
	1. **Database Performance**: Monitoring the database performance helps to understand the performance of the database. It helps to identify the bottlenecks and optimize the database.
	2. **External API Calls**: Monitoring the external API calls helps to understand the performance of the external services. It helps to identify the bottlenecks and optimize the external services.