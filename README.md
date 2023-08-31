# Akamai GTM Load Feedback Object Generator (based off Prometheus Metrics)  

Akamai Global Traffic Management (GTM) is a robust, DNS based global load balancer that offers many performance, geo, availability, and other multi-region routing options.

One powerful feature that GTM includes is the ability for endpoints to publish their real-time capacity, load, and target data, which GTM can then use in making routing decisions. This feature is referred to as "GTM with Load Feedback."

This package scrapes metrics from a managed Kubernetes customer via Prometheus, and creates a load object in XML format that GTM can then read to determine current cluster condition.

This specific implementation requires Prometheus and metrics-server to be installed into your K8s cluster. 

## Getting Started

1. This repository is synced with the brianapley/akamaigtm-loadfeedback-prometheus repository in docker hub. The service can be added to your K8s cluster in a number of ways. Below is an example of creating the service deployment via imperative kubectl commands.

```
kubectl create deploy sidecar --image brianapley/akamaigtm-loadfeedback-prometheus --port=1880
kubectl create svc loadbalancer sidecar --tcp=80:1880
```
2. Once the deployment and service are active, the service UI can be accessed via http://{loadbalancerIP}/ for customization. The data center target percentage, along with the GTM domain and datacenter ID values, need to be manually updated per the instructions in the UI.

![image](https://github.com/ccie7599/akamaigtm-loadfeedback-prometheus/assets/19197357/f4b8e924-1c8c-488f-abe0-90116d175bf0)

3. By default, the service will poll Prometheus every 5 seconds for updated metrics. The load object can be accessed via http://{loadbalancerIP}/loadobject.

## Implementation Details 

* Capacity is determined via the sum(machine_cpu_cores) Prometheus query.
* Load is determined via the sum(rate(node_cpu_seconds_total{mode!="idle"}[2m]))*100 Prometheus query.
* Target is determined by the Capacity x target %. 

## Akamai GTM Configuration

Details on Akamai GTM can be found here - https://techdocs.akamai.com/gtm/docs. A sample Akamai GTM Performance with Load Feedback config is included in this repository (gtmconfig.json).

## Integration with Grafana 

A sample grafana dashboard is included in this repository (dashboard.json). This dashboard includes panes that report on the current Capacity, Load, and Target metrics.

![image](https://github.com/ccie7599/akamaigtm-loadfeedback-prometheus/assets/19197357/b7db658c-d579-4799-8719-4145761ca405)

## To-Dos

1. Hardening of the service itself
2. Automated/streamlined customization of the variable values.
3. Documentation of integration w/ GTM. 
