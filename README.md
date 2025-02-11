## Overview

This project is a comprehensive infrastructure setup for a scalable and highly available environment. It includes configuration files for various services such as DNS, Grafana, InfluxDB, MySQL, and more.

## Architecture

The project is designed to be deployed on multiple servers, with each server playing a specific role. The roles are defined in the `hosts` file and include:

* DNS primary and secondary servers
* Grafana server
* InfluxDB server
* MySQL servers
* Load balancers (HAProxy)
* Prometheus server


## Ansible Playbooks

The project includes Ansible playbooks for automating the deployment and configuration of the services. The playbooks are located in the `roles` directory and include:

* `bind`: DNS playbook
* `grafana`: Grafana playbook
* `influxdb`: InfluxDB playbook
* `mysql`: MySQL playbook
* `haproxy`: HAProxy playbook
* `prometheus`: Prometheus playbook

## Backup and Restore

The project includes a backup and restore process for the MySQL and InfluxDB databases. The backup process is automated using a cron job and the restore process is documented in the `backup_restore.md` file.
