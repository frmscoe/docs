# DNS Monitoring

## Configuration

For DNS Monitoring we require a target to be configured on the Prometheus Config.

```yaml
    - job_name: coredns
      scrape_interval: 5s
      metrics_path: /metrics
      static_configs:
      - targets: ['kube-dns.kube-system.svc:9153']
```

The default Metrics port is: 9153, if you change this, remember to update the target Port. The default service for dns does not expose this port however, so you need to add this to the dns service configuration under specs, ports:  

```yaml
    - name: metrics
      protocol: TCP
      port: 9153
      targetPort: 9153
```

The full object is as follows:  
  

```yaml
spec:
  ports:
    - name: dns
      protocol: UDP
      port: 53
      targetPort: 53
    - name: dns-tcp
      protocol: TCP
      port: 53
      targetPort: 53
    - name: metrics
      protocol: TCP
      port: 9153
      targetPort: 9153
```

### Dashboard

There are numerous dashboards available to monitor Core DNS, the one we’re using has to code: 5926  

```json
{
  "__inputs": [
    {
      "name": "DS_PROMETHEUS",
      "label": "Prometheus",
      "description": "",
      "type": "datasource",
      "pluginId": "prometheus",
      "pluginName": "Prometheus"
    }
  ],
  "__requires": [
    {
      "type": "grafana",
      "id": "grafana",
      "name": "Grafana",
      "version": "4.1.2"
    },
    {
      "type": "panel",
      "id": "graph",
      "name": "Graph",
      "version": ""
    },
    {
      "type": "datasource",
      "id": "prometheus",
      "name": "Prometheus",
      "version": "1.0.0"
    },
    {
      "type": "panel",
      "id": "singlestat",
      "name": "Singlestat",
      "version": ""
    }
  ],
  "annotations": {
    "list": []
  },
  "description": "Bind DNS Service Statistics.rn",
  "editable": true,
  "gnetId": 1666,
  "graphTooltip": 0,
  "hideControls": false,
  "id": null,
  "links": [],
  "rows": [
    {
      "collapse": false,
      "height": "150px",
      "panels": [
        {
          "cacheTimeout": null,
          "colorBackground": false,
          "colorValue": false,
          "colors": [
            "rgba(245, 54, 54, 0.9)",
            "rgba(237, 129, 40, 0.89)",
            "rgba(50, 172, 45, 0.97)"
          ],
          "datasource": "${DS_PROMETHEUS}",
          "decimals": 1,
          "format": "s",
          "gauge": {
            "maxValue": 100,
            "minValue": 0,
            "show": false,
            "thresholdLabels": false,
            "thresholdMarkers": true
          },
          "height": "150",
          "id": 1,
          "interval": null,
          "links": [],
          "mappingType": 1,
          "mappingTypes": [
            {
              "name": "value to text",
              "value": 1
            },
            {
              "name": "range to text",
              "value": 2
            }
          ],
          "maxDataPoints": 100,
          "nullPointMode": "connected",
          "nullText": null,
          "postfix": "s ago",
          "postfixFontSize": "80%",
          "prefix": "",
          "prefixFontSize": "50%",
          "rangeMaps": [
            {
              "from": "null",
              "text": "N/A",
              "to": "null"
            }
          ],
          "span": 3,
          "sparkline": {
            "fillColor": "rgba(31, 118, 189, 0.18)",
            "full": false,
            "lineColor": "rgb(31, 120, 193)",
            "show": false
          },
          "targets": [
            {
              "expr": "max(node_time{alias="openwatt-dns-slave"}) - max(bind_boot_time_seconds{alias="openwatt-dns-slave"})",
              "interval": "5m",
              "intervalFactor": 2,
              "refId": "A",
              "step": 600,
              "target": ""
            }
          ],
          "thresholds": "",
          "title": "Restarted",
          "type": "singlestat",
          "valueFontSize": "80%",
          "valueMaps": [
            {
              "op": "=",
              "text": "N/A",
              "value": "null"
            }
          ],
          "valueName": "avg"
        },
        {
          "cacheTimeout": null,
          "colorBackground": false,
          "colorValue": false,
          "colors": [
            "rgba(245, 54, 54, 0.9)",
            "rgba(237, 129, 40, 0.89)",
            "rgba(50, 172, 45, 0.97)"
          ],
          "datasource": "${DS_PROMETHEUS}",
          "decimals": 1,
          "format": "s",
          "gauge": {
            "maxValue": 100,
            "minValue": 0,
            "show": false,
            "thresholdLabels": false,
            "thresholdMarkers": true
          },
          "height": "150px",
          "id": 2,
          "interval": null,
          "links": [],
          "mappingType": 1,
          "mappingTypes": [
            {
              "name": "value to text",
              "value": 1
            },
            {
              "name": "range to text",
              "value": 2
            }
          ],
          "maxDataPoints": 100,
          "nullPointMode": "connected",
          "nullText": null,
          "postfix": "s ago",
          "postfixFontSize": "80%",
          "prefix": "",
          "prefixFontSize": "50%",
          "rangeMaps": [
            {
              "from": "null",
              "text": "N/A",
              "to": "null"
            }
          ],
          "span": 3,
          "sparkline": {
            "fillColor": "rgba(31, 118, 189, 0.18)",
            "full": false,
            "lineColor": "rgb(31, 120, 193)",
            "show": false
          },
          "targets": [
            {
              "expr": "max(node_time{alias="openwatt-dns-slave"}) - max(bind_config_time_seconds{alias="openwatt-dns-slave"})",
              "interval": "5m",
              "intervalFactor": 2,
              "refId": "A",
              "step": 600,
              "target": ""
            }
          ],
          "thresholds": "",
          "title": "Reconfigured",
          "type": "singlestat",
          "valueFontSize": "80%",
          "valueMaps": [
            {
              "op": "=",
              "text": "N/A",
              "value": "null"
            }
          ],
          "valueName": "avg"
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 3,
          "id": 3,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": false,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 3,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 6,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_process_cpu_seconds_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Named CPU Time",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "s",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 16,
          "legend": {
            "alignAsTable": false,
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "rightSide": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": true,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 4,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "sum(rate(node_cpu{alias="$alias"}[120s])) by (mode) * 100 / count_scalar(node_cpu{mode="user", alias="$alias"}) or sum(irate(node_cpu{alias="$alias"}[120s])) by (mode) * 100 / count_scalar(node_cpu{mode="user", alias="$alias"})",
              "intervalFactor": 2,
              "legendFormat": "{{ mode }}",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "percent",
              "label": null,
              "logBase": 1,
              "max": "100",
              "min": "0",
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": false
            }
          ]
        },
        {
          "aliasColors": {
            "Load 15m": "#CCA300",
            "Load 1m": "#890F02",
            "Load 5m": "#C15C17"
          },
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 17,
          "legend": {
            "alignAsTable": false,
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "rightSide": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 2,
          "links": [],
          "nullPointMode": "null",
          "percentage": true,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 4,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "expr": "node_load1{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Load 1m",
              "refId": "A",
              "step": 10,
              "target": ""
            },
            {
              "expr": "node_load5{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Load 5m",
              "refId": "B",
              "step": 10,
              "target": ""
            },
            {
              "expr": "node_load15{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Load 15m",
              "refId": "C",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": "0",
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": false
            }
          ]
        },
        {
          "aliasColors": {
            "Load 15m": "#CCA300",
            "Load 1m": "#890F02",
            "Load 5m": "#C15C17"
          },
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 5,
          "id": 18,
          "legend": {
            "alignAsTable": false,
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "rightSide": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 4,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "node_memory_MemTotal{alias="$alias"} - (node_memory_MemFree{alias="$alias"} + node_memory_Buffers{alias="$alias"} + node_memory_Cached{alias="$alias"})",
              "intervalFactor": 2,
              "legendFormat": "Used",
              "refId": "A",
              "step": 10,
              "target": ""
            },
            {
              "expr": "node_memory_MemFree{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Free",
              "refId": "B",
              "step": 10,
              "target": ""
            },
            {
              "expr": "node_memory_Buffers{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Buffers",
              "refId": "C",
              "step": 10,
              "target": ""
            },
            {
              "expr": "node_memory_Cached{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Cached",
              "refId": "D",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": [
              "total"
            ]
          },
          "yaxes": [
            {
              "format": "bytes",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": "0",
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": false
            }
          ]
        }
      ],
      "repeat": null,
      "repeatIteration": null,
      "repeatRowId": null,
      "showTitle": false,
      "title": "Dashboard Row",
      "titleSize": "h6"
    },
    {
      "collapse": false,
      "height": 250,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 4,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 2,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [
            {
              "alias": "Max File Descriptors",
              "fill": 0
            }
          ],
          "span": 6,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "expr": "bind_process_max_fds{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Max",
              "refId": "A",
              "step": 10,
              "target": ""
            },
            {
              "expr": "bind_process_open_fds{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Open",
              "refId": "B",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "File Descriptors",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 32,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {
            "Resident": "#890F02",
            "Virtual": "#0A437C",
            "Virtual Memory": "#0A437C"
          },
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 2,
          "id": 5,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 3,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 6,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "expr": "bind_process_virtual_memory_bytes{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Virtual",
              "refId": "A",
              "step": 10,
              "target": ""
            },
            {
              "expr": "bind_process_resident_memory_bytes{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "Resident",
              "refId": "B",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Memory",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "bytes",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        }
      ],
      "repeat": null,
      "repeatIteration": null,
      "repeatRowId": null,
      "showTitle": false,
      "title": "Dashboard Row",
      "titleSize": "h6"
    },
    {
      "collapse": false,
      "height": 250,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 6,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "rightSide": true,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 6,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_incoming_queries_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ type }}",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Incoming Queries",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 7,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "rightSide": true,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 6,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_incoming_requests_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ opcode }}",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Incoming Request Opcodes",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 8,
          "legend": {
            "alignAsTable": true,
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "rightSide": true,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 12,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_responses_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ result }}",
              "refId": "A",
              "step": 4,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Response Results",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        }
      ],
      "repeat": null,
      "repeatIteration": null,
      "repeatRowId": null,
      "showTitle": false,
      "title": "Dashboard Row",
      "titleSize": "h6"
    },
    {
      "collapse": false,
      "height": 250,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 9,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 12,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_query_duplicates_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "Duplicates",
              "refId": "A",
              "step": 4,
              "target": ""
            },
            {
              "expr": "increase(bind_query_errors_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ error }}",
              "refId": "B",
              "step": 4,
              "target": ""
            },
            {
              "expr": "increase(bind_query_recursions_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "Recursions",
              "refId": "C",
              "step": 4,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Queries",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        }
      ],
      "repeat": null,
      "repeatIteration": null,
      "repeatRowId": null,
      "showTitle": false,
      "title": "Dashboard Row",
      "titleSize": "h6"
    },
    {
      "collapse": false,
      "height": 250,
      "panels": [
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 10,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 6,
          "stack": false,
          "steppedLine": false,
          "targets": [
            {
              "expr": "bind_resolver_cache_rrsets{alias="$alias"}",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / {{ type }}",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Resolver Cache RR Sets",
          "tooltip": {
            "shared": true,
            "sort": 0,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 11,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 6,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_resolver_dnssec_validation_errors_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / ValErr",
              "refId": "A",
              "step": 10,
              "target": ""
            },
            {
              "expr": "increase(bind_resolver_dnssec_validation_success_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / {{ result }}",
              "refId": "B",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "DNSSEC Validation",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 12,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 4,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_resolver_queries_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / {{ type }}",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Resolver Queries",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 13,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 4,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_resolver_query_errors_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / {{ error }}",
              "refId": "A",
              "step": 10,
              "target": ""
            },
            {
              "expr": "increase(bind_resolver_query_edns0_errors_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / EDNS0",
              "refId": "B",
              "step": 10,
              "target": ""
            },
            {
              "expr": "increase(bind_resolver_query_retries_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / Retry",
              "refId": "C",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Query Errors",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 14,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 4,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_resolver_query_duration_seconds_bucket{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / {{ le }}",
              "refId": "A",
              "step": 10,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Query By Duration",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        },
        {
          "aliasColors": {},
          "bars": false,
          "datasource": "${DS_PROMETHEUS}",
          "fill": 1,
          "id": 15,
          "legend": {
            "avg": false,
            "current": false,
            "max": false,
            "min": false,
            "show": true,
            "total": false,
            "values": false
          },
          "lines": true,
          "linewidth": 1,
          "links": [],
          "nullPointMode": "null",
          "percentage": false,
          "pointradius": 5,
          "points": false,
          "renderer": "flot",
          "seriesOverrides": [],
          "span": 12,
          "stack": true,
          "steppedLine": false,
          "targets": [
            {
              "expr": "increase(bind_resolver_response_errors_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / {{ error }}",
              "refId": "A",
              "step": 4,
              "target": ""
            },
            {
              "expr": "increase(bind_resolver_response_lame_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / LAME",
              "refId": "B",
              "step": 4,
              "target": ""
            },
            {
              "expr": "increase(bind_resolver_response_mismatch_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / MISMATCH",
              "refId": "C",
              "step": 4,
              "target": ""
            },
            {
              "expr": "increase(bind_resolver_response_truncated_total{alias="$alias"}[120s])",
              "intervalFactor": 2,
              "legendFormat": "{{ view }} / TRUNCATED",
              "refId": "D",
              "step": 4,
              "target": ""
            }
          ],
          "thresholds": [],
          "timeFrom": null,
          "timeShift": null,
          "title": "Resolver Response Errors",
          "tooltip": {
            "shared": true,
            "sort": 2,
            "value_type": "individual"
          },
          "type": "graph",
          "xaxis": {
            "mode": "time",
            "name": null,
            "show": true,
            "values": []
          },
          "yaxes": [
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            },
            {
              "format": "short",
              "label": null,
              "logBase": 1,
              "max": null,
              "min": null,
              "show": true
            }
          ]
        }
      ],
      "repeat": null,
      "repeatIteration": null,
      "repeatRowId": null,
      "showTitle": true,
      "title": "Resolver",
      "titleSize": "h6"
    }
  ],
  "schemaVersion": 14,
  "style": "dark",
  "tags": [
    "dns",
    "bind",
    "prometheus"
  ],
  "templating": {
    "list": [
      {
        "allValue": null,
        "current": {},
        "datasource": "${DS_PROMETHEUS}",
        "hide": 0,
        "includeAll": false,
        "label": "Host",
        "multi": false,
        "name": "alias",
        "options": [],
        "query": "label_values(bind_up, alias)",
        "refresh": 1,
        "regex": "",
        "sort": 1,
        "tagValuesQuery": "",
        "tags": [],
        "tagsQuery": "",
        "type": "query",
        "useTags": false
      }
    ]
  },
  "time": {
    "from": "now-1h",
    "to": "now"
  },
  "timepicker": {
    "refresh_intervals": [
      "5s",
      "10s",
      "30s",
      "1m",
      "5m",
      "15m",
      "30m",
      "1h",
      "2h",
      "1d"
    ],
    "time_options": [
      "5m",
      "15m",
      "1h",
      "6h",
      "12h",
      "24h",
      "2d",
      "7d",
      "30d"
    ]
  },
  "timezone": "browser",
  "title": "Bind DNS",
  "version": 29
}
```
