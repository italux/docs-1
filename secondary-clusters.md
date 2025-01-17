Secondary Clusters Guide
===================

Secondary clusters use a minimal Kubecost deployment to send their metrics to a central storage-bucket (aka durable storage) that is accessed by the primary cluster to provide a ___single-pane-of-glass___ view into all aggregated cluster costs globally. This aggregated cluster view is exclusive to Kubecost Enterprise.

> **Note**: The UI on secondary clusters will appear broken. It is meant for troubleshooting only.

This guide explains settings that can be tuned in order to run the minimum Kubecost components to run Kubecost more efficiently. 

See the [additional resources](/architecture/secondary-clusters#additional-resources) section below for complete examples in our github repo.

## Kubecost Global

Disable product caching and reduce query concurrency with the following parameters:

```
--set kubecostModel.warmCache=false
--set kubecostModel.warmSavingsCache=false
--set kubecostModel.etl=false
--set kubecostModel.etlCloudAsset
--set kubecostModel.maxQueryConcurrency=1
```

## Grafana

Grafana is not needed on secondary clusters.

```
--set global.grafana.enabled=false
--set global.grafana.proxy=false
```

## Prometheus

Kubecost and its accompanying Prometheus collect a reduced set of metrics that allow for lower resource/storage usage than a standard Prometheus deployment.

The following configuration options further reduce resource consumption when not using the Kubecost frontend:

```sh
--set prometheus.server.retention=2d
```

Potentially reducing retention even further, metrics are sent to the storage-bucket every 2 hours.

You can tune prometheus.server.persistentVolume.size depending on scale, or outright disable persistent storage.

## Thanos

Disable Thanos components. These are only used for troubleshooting on secondary clusters. See this guide for [troubleshooting via kubectl logs](/install-and-configure/install/long-term-storage#troubleshooting).

> **Note**: Secondary clusters write to the global storage-bucket via the thanos-sidecar on the prometheus-server pod.

```sh
--set thanos.compact.enabled=false
--set thanos.bucket.enabled=false
--set thanos.query.enabled=false
--set thanos.queryFrontend.enabled=false
--set thanos.store.enabled=false
```

## Node-Exporter

You can disable node-exporter and the service account if cluster/node rightsizing recommendations are not required.

> **Note**: node-export must be disabled if there is an existing daemonset. More info [here](/troubleshooting/troubleshoot-install#issue-failedscheduling-kubecost-prometheus-node-exporter).

## Helm values

For reference, this is a list of the most common settings for efficient secondary clusters:

`secondary-clusters.yaml`
```yaml
kubecostProductConfigs:
  clusterName: kubecostProductConfigs_clusterName
kubecostModel:
  warmCache: false
  warmSavingsCache: false
  etl: false
  etlCloudAsset: false
  maxQueryConcurrency: 1
global:
  grafana:
    enabled: false
    proxy: false
prometheus:
  server:
    global:
      external_labels:
        # cluster_id should be unique for all clusters and the same value as .kubecostProductConfigs.clusterName
        cluster_id: kubecostProductConfigs_clusterName
    retention: 2d
  # nodeExporter:
  #   enabled: false
  # serviceAccounts:
  #   nodeExporter:
  #     create: false
thanos:
  compact:
    enabled: false
  bucket:
    enabled: false
  query:
    enabled: false
  queryFrontend:
    enabled: false
  store:
    enabled: false
```

## Additional resources

You can find complete installation guides and sample files on our [repo](https://github.com/kubecost/poc-common-configurations)

Additional considerations for properly tuning resource consumption is [here](/general/resource-consumption).

## Help
<a name="help"></a>
There are potentially other configuration options based on the specifics of different deployment requirements. Reach out to us if you run into any issues, we are here to help!

[Slack community](https://join.slack.com/t/kubecost/shared_invite/zt-1dz4a0bb4-InvSsHr9SQsT_D5PBle2rw) - check out #support for any help you may need & drop your introduction in the #general channel

Write to us at [support@kubecost.com](support@kubecost.com).
