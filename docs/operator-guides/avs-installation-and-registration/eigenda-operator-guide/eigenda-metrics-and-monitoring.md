---
description: Setup Grafana and Prometheus Metrics and Monitoring Stack
---

# EigenDA Metrics and Monitoring

These instructions provide a quickstart guide to run the Prometheus, Grafana, and Node exporter stack.

**Step 1:** Move your current working directory to the monitoring folder:

```
cd monitoring
```

- Open the `.env` file, ensure the location of `prometheus.yml` is correct for your environment.
- In the `prometheus.yml` file:
  - Update prometheus config [file](https://github.com/Layr-Labs/eigenda-operator-setup/blob/master/monitoring/prometheus.yml) is updated with the metrics port (`NODE_METRICS_PORT`) of the eigenda node in parent folder `.env` file
  - Ensure the eigenda container name for `scrape_configs.targets` matches the value of the parent folder `.env` file (`MAIN_SERVICE_NAME`).
  - Make sure the location of prometheus file is correct in [.env](https://github.com/Layr-Labs/eigenda-operator-setup/blob/master/monitoring/.env) file

**Step 2:** Run the following command to start the monitoring stack

```
docker compose up -d
```

**Step 3:** Since eigenda is running in a different docker network we will need to have prometheus in the same network. To do that, run the following command

```
docker network connect eigenda-network prometheus
```

Note: eigenda-network is the name of the network in which eigenda is running. You can check the network name in eigenda [.env](https://github.com/Layr-Labs/eigenda-operator-setup/blob/master/.env#L2) file (`NETWORK_NAME`). This will ensure Prometheus can scrape the metrics from Eigenda node.

Useful Dashboards: we also provide a set of useful Grafana dashboards which would be useful for monitoring the EigenDA node. You can find them [here](https://github.com/Layr-Labs/eigenda-operator-setup/tree/master/dashboards). Once you have Grafana setup, feel free to import the dashboards.

If you prefer to set up the metrics and monitoring stack manually, follow the steps located [here](https://github.com/Layr-Labs/eigenda-operator-setup#metrics).
