Observability is the ability of to collect data about the program's execution, internal states, and communication among components. Usually wide range of logging and tracing techniques are used to gather telemetry information.

## Monitoring vs Observability
Main difference between monitoring and observability is that monitoring is focused on "is the system running well?" while observability is focused on "why is the system not running well?".
So, the observability is more focused on collecting and analyzing how the application behaves in production.
## Telemetry Types
Telemetry informations is automated process of measuring and remotely transmitting data. There are several types of telemetry information:
- **Metrics**: 
	Metrics are point in time data that can be aggregated and visualized. The common metrics includes:
	- Number of HTTP requests per second
	- Total of number query failed
	- Database size in bytes
- **Logs**: 
	Logs, or log lines, are generally free-form text that are written to a file or stream. Logs typically include timestamp and severity level. The common logs includes: 
	- Error logs
	- Debug logs 
	- Info logs
- **Traces**: 
	Traces are a collection of events that are generated by a single request as it flows through a system. Traces are used to understand the flow of requests through the system. To be able to follow a request through the system, each span in the trace has a unique identifier that is passed between services.
- **Continuous Profiling**:
	Continuous profiling is a way to collect precise information about how the application consuming resources. Continuous profiling is used to understand the performance of the application and identify the bottlenecks.
- **Instrumentation**: 
	To be able to observe application, telemetry information is required to be collected and exported from the application. Instrumentation means generating telemetry information from the application during normal operation. 
	Instrumentation could be automatic or manual. Automatic instrumentation offers blanket coverage of the application, while manual instrumentation requires developer to add telemetry information to the codebase.
    Instrumentation also could be native (done-in-code) or non-native (out-of-code). The example of non-native instrumentation is using APM (Application Performance Monitoring) tools like New Relic, Datadog, or AppDynamics. The example of native instrumentation is using OpenTelemetry.

