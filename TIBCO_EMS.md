#  Datadog Setup for TIBCO EMS
## Implementation with Datadog Platform for Observability
### Datadog Agent Install 
- Install the [Datadog Agent](https://docs.datadoghq.com/agent/) on each server. 
This will link the server (or Cloud resource) to Datadog and provide the ablity to gather metrics, status of server, processes, network and more. 

### Information Gathered on TIBCO EMS: 
- Defined as "a standard-based messaging platform built around supporting JMS 1.1 and 2.0 standards. TIBCO Enterprise Message Service is TCK certified for both JMS 1.1 and 2.0." - src TIBCO Software Wiki
  - Datadog [Java APM Library](https://docs.datadoghq.com/tracing/setup_overview/compatibility_requirements/java/#networking-framework-compatibility) supports the Java Message Service (JMS) versions 1 & 2 with full support and Spring SessionAwareMessageListner 3.1+ (spring-jms-3.1). 

### Setup instructions for Datadog Java (.jar) and TIBCO EMS: 
- According to the TIBCO documentation: 
   - [Enable the JVM](https://docs.tibco.com/pub/ems/latest/doc/html/GUID-2C438D30-3692-4655-8859-4B4FF9A0378A.html) - states that the EMS server can run the JVM by enabling the following:  
      - `jre_library = path`
        - _"Enables the JVM in the EMS server, where the path is absolute path to the JRE shared library file that is installed with the JRE"_ - src [jre_library](https://docs.tibco.com/pub/ems/latest/doc/html/GUID-29D232BA-A3FF-4144-A2FD-2B926DE42DCA.html) 
      - `jre_options = JVMOptions`
        - _"The `jre_option` parameter can be used to define Java system properties, which are used by applications running in the JVM"_ - src [jre_option](https://docs.tibco.com/pub/ems/latest/doc/html/GUID-D03822A9-A25B-4BD1-93F6-F250699DE55B.html)
- Datadog Java Library setup 
   - The Datadog Java Library (.jar) and the Java tracer's system properties can be passed into the `jre_option` within your EMS server's [tibemsd.conf](https://docs.tibco.com/pub/ems/latest/doc/html/GUID-65F2F184-5591-4CDF-88F0-5E9240AB8170.html) file.
      - An example value would be: 
         - jre_option=`'-javaagent:/usr/local/datadog/lib/dd-java-agent.jar' '-Ddd.service=tibco_ems' '-Ddd.version=1.0' '-Ddd.env=uat'`
      - Please be sure to restart the EMS server for the changes to be accepted. 

