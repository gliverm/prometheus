# prometheus

Prototype for learning.

Goal: Figure out how to monitor interesting host and app telemetry metrics.

* Info for build and run of experimental Dockerfiles are within the files
* To check config files: promtool check config <config.yml>
* To see prometheus server stats: localhost:9090/metrics
* Use prometheous explorer to 'test' out PromQL selectors


Example of selectors:

* Free memory in bytes for a specific instance: node_memory_MemFree_bytes{instance="10.243.241.222:9100"}
* Available memory in bytes: node_memory_MemAvailable_bytes
