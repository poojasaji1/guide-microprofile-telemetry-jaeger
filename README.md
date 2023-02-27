# draft-microprofile-telemetry

## MicroProfile Telemetry 1.0
Create and Manage traces using OpenTelemetry open standards 


# What you’ll learn 

The use of microservices architecture may increase difficultly to see how services depend on or affect other services. Consequently, making it harder to find the source of latency or inaccuracy.
One way to increase observability of an application is by emitting traces. OpenTelemetry is a set of APIs, SDKs, tooling and integrations that are designed for the creation and management of telemetry data such as traces, metrics, and logs. MicroProfile Telemetry 1.0 adopts OpenTelemetry so your MicroProfile applications can benefit from both manual and automatic traces!

Traces represent requests and consist of multiple spans.
Spans are representative of single operations in a request and contain a name, time-related data, log messages and metadata to give information about what occurs during a transaction.
Context is an immutable object contained in the span data to identify the unique request that each span is a part of. This data is required for moving trace information across service boundaries, allowing developers to follow a single request through a potentially complex distributed system.
Exporters are components that send data to a backend service so you can visualise and monitor the generated spans.

You can export the data that MicroProfile Telemetry 1.0 collects to Jaeger or Zipkin. Additionally, OpenTelemetry includes a simple logging exporter, which provides an easy way to check that spans are being created by viewing the data in your console. This may be helpful for debugging

You’ll configure the provided inventory and system services to use Jaeger/Zipkin for distributed tracing with MicroProfile OpenTracing. You’ll run these services in two separate JVMs made of two server instances to demonstrate tracing in a distributed environment. If all the components were run on a single server, then any logging software would be sufficient.

# Additional prerequisites 

Before you begin, make sure you have all the necessary prerequisites.

Jaeger:
Before you begin, deploy the Jaeger all-in-one executable file to start the Jaeger tracing system. The Jaeger all-in-one executable file is configured for quick local testing. You can find information about the Jaeger server and instructions for starting the all-in-one executable file in the Jaeger documentation.
Before you proceed, make sure that your Jaeger server is up and running. Jaeger can be found at the http://localhost:16686 URL.

Zipkin:
For this guide, Zipkin is used as the distributed tracing system. You can find the installation instructions for Zipkin at the Zipkin quickstart page. You’re not required to use Zipkin. You may choose to use another tracing system. However, this guide is written using Zipkin. If you use a different tracing system, the required instructions may differ.
Before you continue, confirm your Zipkin server is up and running. By default, Zipkin can be found at the http://localhost:9411 URL.

# Getting started 

The fastest way to work through this guide is to clone the Git repository and use the projects that are provided inside:

```
git clone https://github.com/openliberty/guide-microprofile-opentelemetry-jaeger.git
cd guide-microprofile-opentelemetry-zipkin
```

Or 
```
git clone https://github.com/openliberty/guide-microprofile-opentelemetry-jaeger.git
cd guide-microprofile-opentelemetry-zipkin
```

The start directory contains the starting project that you will build upon.

The finish directory contains the finished project that you will build.

Before you begin, make sure you have all the necessary prerequisites.
	# Try what you’ll build

Start the system service:

```
mvn liberty:run
```

Navigate to the system properties endpoint:

http://localhost:9080/system/properties

A span for this request will be created by the Java Agent. Check for the span in the exporter’s endpoint.

MicroProfile Telemetry 1.0 allows you to observe traces without modifying source code in your Jakarta RESTful web service (aka JAX-RS) applications.
As you can see in the inventory service, you can enable mpTelemetry-1.0 in your server.xml:

```
<featureManager>
  <feature>mpTelemetry-1.0</feature>
</featureManager>
```

By default, MicroProfile Telemetry tracing is off. To enable any tracing aspects, specify ```otel.sdk.disabled=false``` as a config property or ```OTEL_SDK_DISABLED=false``` as an environment property for your server.

Open a new command-line session and navigate to the inventory directory:

```
cd inventory
```
Run the following Maven goal to build the inventory service and deploy it to Open Liberty:
```
mvn liberty:run
```
Navigate to the inventory endpoint:

http://localhost:9081/inventory/systems/localhost

You should see 3 spans in the exporter’s endpoint: two spans from inventory and one span from system.

Stop the inventory service by pressing ```Ctrl+c``` in the terminal session.

You have collected traces using the Java Agent and Automatic Instrumentation!


# Building the application 

# Enabling the existing Telemetry implementation 

# Enabling and disabling the distributed …

# Testing the services 

No automated tests are provided to verify the correctness of the traces. Manually verify these traces by viewing them on the Jaeger/Zipkin server.
A few tests are included for you to test the basic functionality of the services. If a test failure occurs, then you might have introduced a bug into the code.

	# Running the tests

Since you started Open Liberty in dev mode, run the tests for the system and inventory services by pressing the enter/return key in the command-line sessions where you started the services.

When you are done checking out the services, exit dev mode by pressing ```CTRL+C``` in the shell sessions where you ran the system and inventory services, or by typing ```q``` and then pressing the ```enter/return``` key.

Finally, stop the Jaeger/Zipkin service that you started in the Additional prerequisites section.
