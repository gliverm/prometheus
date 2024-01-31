# prometheus

Prototype for learning.  Pluralsight has some great tutorials that jumpstarted mylearning.

Goal: Figure out how to monitor interesting host and app telemetry metrics.

* Info for build and run of experimental Dockerfiles are within the files
* To check config files: promtool check config <config.yml>
* To see prometheus server stats: localhost:9090/metrics
* Use prometheous explorer to 'test' out PromQL selectors

## Starting Environment

1. Modify the prometheus directory with the values needed to connect to your devices
2. Start the docker detached enviornment: `docker-compose up -d`
3. Browse to Grafana: `http://localhost:3000`
   1. Login creds: admin/admin
   2. Don't bother changing the admin creds
4. Browse to Prometheus: 'http://localhost:9090'
5. Connect containerized Prometheus to containerized Grafana
   1. From menu: Connections > Data sources
   2. Choose Prometheus under Time series databases section
   3. Modify the Connection URL using the container name for the prometheus server to: http://prometheus:9090
   4. Scroll down to end of page and click save and test - the result shoudl be successfully queried

## Stopping Environment

* Stop and discard containers and network: `docker-compose down`
* Hault the environment not discarding containers: `docker-compose stop`

## Learning Selectors

* Free memory in bytes for a specific instance: node_memory_MemFree_bytes{instance="10.243.241.222:9100"}
* Available memory in bytes: node_memory_MemAvailable_bytes
