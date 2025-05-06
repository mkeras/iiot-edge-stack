# iiot-edge-stack
Demo docker stack for edge devices. Uses: HiveMQ Edge and timebase historian to historize sparkplug b tags


## Prerequisites
- docker and docker compose


## How to use
### 1) Clone repository: `git clone https://github.com/mkeras/iiot-edge-stack`
---
### 2) Change directory to the repo: `cd iiot-edge-stack`
---
### 3) Create the docker network: `docker network create iiot-edge-net`
This creates the internal docker network that the containers will use to communicate to each other.

---
### 4) Start the core services: `docker compose up -d`
This command will start the HiveMQ Edge, Timebase Historian, and Timebase Explorer containers. The default mapped host ports are set in the .env file next to the docker-compose.yml. They are:
- Timebase Historian: 4511 (.env TB_HISTORIAN_PORT_EXTERNAL)
- Timebase Explorer: 4531 (.env TB_EXPLORER_PORT_EXTERNAL)
- HiveMQ Edge: 6001 for the web interface (.env HIVEMQ_ADMIN_PORT) and 1883 for MQTT (.env MQTT_PORT).

---
### 5) Start the collector(s)
Please note that only the Sparkplug B has been tested/configured correctly to work with this stack so far. To start a collector simply docker compose up, specifying collector's directory. For example, the sparkplug b collector: `docker compose -f "historian-timebase/collectors/sparkplugb/docker-compose.yml" up -d`

---
### 6) Done
Once these steps are complete and the sparkplugb collector is running, your host machine is ready to accept mqtt connections on port 1883 and is ready to historize any sparkplug b payloads via timebase. The Dataset name of the Sparkplug B collector is SPB_DEMO. This can be changed in via the file: <br>`historian-timebase/collectors/sparkplugb/data/config/collector.config`

## See also:
### [Timebase Documentation](https://timebase.flow-software.com/en/knowledge-base/start-here)
### [HiveMQ Edge Documentation](https://docs.hivemq.com/hivemq-edge/)