# eck-fleet-and-elastic-agent

_(Work in Progress)_

This page will guide you through how to configure elastic agent with fleet managed mode using ECK.
Elastic agent is a unified way to collect logs and metrics and ship them to elasticsearch, basically, instead of configuring filebeat and metricbeat, you can now choose by install only Elastic agent in your host.
On the other hand, Fleet is a Kibana UI to add and manage elastic agents.

## Jumping into it
First thing first, let's deploy our elasticsearch cluster by applying the [es.yml](https://github.com/framsouza/eck-fleet-and-elastic-agent/blob/main/es.yml) file.
There's nothing to care about on this manifest, this is pretty straightforward, contains only the resource request/limit (very important to set it) and the vm.max_map_count adjustment. 

Next step is deploy Kibana by applying the [kibana.yml](https://github.com/framsouza/eck-fleet-and-elastic-agent/blob/main/kibana.yml)
There are two lines to pay attention here:

```
 config:
	 xpack.fleet.agents.elasticsearch.host: "https://cluster1-es-http.default.svc:9200"
	 xpack.fleet.agents.fleet_server.hosts: ["https://fleet-server-agent-http.default.svc:8220"]
```

