
## Dashboard Redesign Notes

### Overview
As an Aerospike oeprator I need an at a glance view that can be used to see across multiple clusters, and see within specific clusters without seeing specifics about namespaces, or sets. 

* Include an Aerospike logo.
* See currently firing critical alerts across all clusters. I don't think there is a way to link from the Alerts List module.
* A list of all (new) dashboards
* See how many clusters you have and how big they are and what version they are and what thier names are (if present). Clicking on them should take you to a Cluster Config Dashboard.
* Quickly see how much unique data you have across all clusters in a single display. Clicking on this panel should go to the Unique Data usage dashboard.
* See how many nodes you have and what the network traffic is to/from them using a visual display using a 
* Overall Read / Writes

Notes: This should take the place of the Cluster Overview dashboard. 

### Namesace and Set Dashboard
As an aerospike customer I need to be able to see namespace and set level information easily.

* ability to filter by cluster and ns

* read / writes 
* timeseries list of top unique data (bytes) by cluster
* timeseries list of top unique data (bytes) by namespaces

* MasterObjects per namespace

```json
{"time":"2023-02-03T11:13:42-08:00","hours_since_start":0,"cluster_name":"null","cluster_generation":1,"cluster_stable":true,"node_count":1,"level":"info","master_objects":2,"unique_data_bytes":178,  "namespaces":{"test":{"master_objects":2,"unique_data_bytes":178}},"errors":[]}
```

```
rate(aerospike_namespace_client_read_success{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_read_timeout{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_read_error{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_read_not_found{ cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_read_success{ cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_read_error{ cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_read_timeout{ cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_read_not_found{ cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m])
```

```
rate(aerospike_namespace_client_write_success{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_write_timeout{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_write_error{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_write_success{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_write_timeout{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_write_error{cluster_name=~"$cluster", ns=~"$namespace|$^"}[1m])
```

```
rate(aerospike_namespace_client_write_success{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_write_timeout{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m])+rate(aerospike_namespace_client_write_error{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_write_success{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_write_timeout{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m]) + rate(aerospike_namespace_batch_sub_write_error{cluster_name=~"$cluster",  ns=~"$namespace|$^"}[1m])
```



* See how many namespaces you have and how big they are

* Be able to toggle to specific clusters (Variable)

Node Overview - Get a node specific view of details on
* Network in / out
* Number of connections / Clients
* Read / write
* Memory
* CPU

Namespace & Sets


Users/Clients / Quotas


