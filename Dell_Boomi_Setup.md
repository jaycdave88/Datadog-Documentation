#  Datadog Setup for Boomi Observability
## Implementation with Datadog Platform for Observability
### Datadog Agent Install 
- Install the [Datadog Agent](https://docs.datadoghq.com/agent/) on each server. 
This will link the server (or Cloud resource) to Datadog and provide the ablity to gather metrics, status of server, processes, network and more. 

### Log Configuration
- To configure the Datadog agent to tail the Boomi logs the following configuration can be used. 

Please note: Boomi offers 6 different types of logs. 
- containers
- shared web server
- api gateway
- api gateway access 
- api portal 
- auth broker

For the purposes of this example we will show configuration for the container & shared http server logs. 

- Within the Datadog Agent conf.d directotry add the following: `/etc/datadog-agent/conf.d/boomi.d/conf.yaml`

```
logs:
  - type: file
    path: /mnt/nfs/centos_molecule/Boomi_AtomSphere/Molecule/Molecule_centos_linux_cluster/logs/*.container.192_168_0_119.log
    service: boomimolecule
    source: boomi-container
    log_processing_rules:
      - type: multi\_line
        name: boomi-container-startwithdate
        pattern: \\w{3}\\s+\\d{2},
    
  - type: file
    path: /mnt/nfs/centos_molecule/Boomi_AtomSphere/Molecule/Molecule_centos_linux_cluster/logs/*.shared_http_server.192_168_0_119.log
    service: boomimolecule
    source: boomi-sharedwebserver
```
### APM Setup
- The [Datadog Java Tracing Library](https://github.com/DataDog/dd-trace-java/releases) (.jar) needs to be deployed on each node or deployed on the Shared Server accessiable by all nodes. 
- Once complete the following Boomi System properties need to be updated via Boomi AtomSphere: 

Select Add a Property and add each of the following properties
```
-DIMMEDIATE_PREFETCH=true
-Ddd.env={{Env} (see chart below)
-Ddd.logs.injection=true
-Ddd.profiling.enabled=true
-Ddd.service=boomiatom
-Ddd.trace.methods=com.boomi.execution.ExecutionTask[call];
-Ddd.version=1.0
-Djava.compiler=NONE
-XX:FlightRecorderOptions=stackdepth=256
-javagent:{{DdJarPath}}
```
Please note: The property `-javaagent` utilizes an absolute path to the jar so you must enter the appropriate path.
