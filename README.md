# ODALA Mobility Dashboard

## Run locally

```sh
docker compose up
```

Grafana is running at http://localhost:3000

Grafana default user/pass is admin/odala2, it can be changed in the settings

## About the datasource

The grafana datasource used to make NGSI-LD native queries is https://github.com/zarelit/ngsild-grafana-datasource/tree/scorpio_support .
This is a derivative of the original https://github.com/bfi-de/ngsild-grafana-datasource that works around a limitation of the method used to check the availability of the broker, which is  Orion-LD specific.

Other quirks are:

1. NGSI-LD does not mandate any endpoint that responds 200 with an empty broker (i.e. no entities), so the DS works only with non-empty brokers.
2. Scorpio returns `attributeNames = <string>` instead of `attributeNames = [<string>]` . See https://github.com/ScorpioBroker/ScorpioBroker/issues/381
3. The datasource is stripping part of the path from the timeseries URL so we must append `ngsi-ld/v1` explicitly in the configuration