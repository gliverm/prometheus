# prometheus

Prototype for learning.  Pluralsight has some great tutorials that jumpstarted my learning.

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
   4. Scroll down to end of page and click save and test - the result should be successfully queried

## Stopping Environment

* Stop and discard containers and network: `docker-compose down`
* Halt the environment not discarding containers: `docker-compose stop`

## Set up Node Exporter on Linux System

Servers exist in author's environment with node-exporter already installed.  Information as to how to set up a linux system can be found on the  Prometheus web site as a [guide](https://prometheus.io/docs/guides/node-exporter/#installing-and-running-the-node-exporter).  Steps to install on a Linux box follow.  Reference [link](https://docs.vmware.com/en/VMware-vRealize-Operations-Management-Pack-for-Kubernetes/1.8.1/management-pack-for-kubernetes/GUID-A1B68BE5-EF38-48E1-AA80-FD71E6F19989.html).

1. Download and move node exporter binary

   `wget <download link> tar xvfz node_exporter-*.*-amd64.tar.gz sudo mv node_exporter-*.*-amd64/node_exporter /usr/local/bin/`
2. Create user to run node_exporter as a service.

   `sudo useradd -rs /bin/false node_exporter`
3. Create service file.

   ```
   sudo tee /etc/systemd/system/node_exporter.service<<EOF
   [Unit]
   Description=Node Exporter
   After=network.target

   [Service]
   User=node_exporter
   Group=node_exporter
   Type=simple
   ExecStart=/usr/local/bin/node_exporter

   [Install]
   WantedBy=multi-user.target
   EOF
   ```
4. Reload system daemon and start the node_exporter service.
   `sudo systemctl daemon-reload sudo systemctl start node_exporter sudo systemctl enable node_exporter`
5. Check the status of node exporter service.
   `sudo systemctl status node_exporter`
6. Verify node_exporter is URL is working.
   `http://<Node-IP>:9100/metrics`

## Community Linux Server Dashboard

Suggest downloading a community version of a dashboard to learn from.  Community dashboards may be found on the Grafana site under dashboards.  An interesting dashboard to experiment with may be the one labeled 'node exporter full'.  Because this setup is intended to be for experimenting, it may also be worth the time to mess with how to export and re-import configuration data to be able to recreate.

## Learning Selectors

* Free memory in bytes for a specific instance: node_memory_MemFree_bytes{instance="10.243.241.222:9100"}
* Available memory in bytes: node_memory_MemAvailable_bytes
