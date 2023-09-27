# ODALA Mobility Dashboard

## Run locally

```sh
docker compose up
```

Grafana is running at <http://localhost:3000>

Grafana default user/pass is admin/odala2, it can be changed in the settings

## Deployment on kubernetes

Under `kubernetes/` there is a kustomization bundle.
Change the values through the overlay, then `kubectl apply -k kubernetes/overlay`

The dashboard will query Scorpio for entities of type OnStreetParking, OffStreetParking, RestrictedTrafficArea
and GtfsStop. Info about the datamodels can be found here: <https://github.com/smart-data-models>

In the case of the city of Arezzo the data comes from the following extractors:

- https://gitlab.publiccode.solutions/odala/otp-stops-extractor
- https://gitlab.publiccode.solutions/odala/emixer-fetcher

Refer to those repositories if data can be ingested from the same providers.

## About the datasource

The grafana datasource used to make NGSI-LD native queries is
<https://gitlab.publiccode.solutions/odala/ngsild-grafana-datasource> .

This is a derivative of the original <https://github.com/bfi-de/ngsild-grafana-datasource>
that works around a limitation of the method used to check the availability of
the broker, which is  Orion-LD specific.

Other quirks are:

1. NGSI-LD does not mandate any endpoint that responds 200 with an empty broker
   (i.e. no entities), so the DS works only with non-empty brokers.
2. Scorpio returns `attributeNames = <string>` instead of
   `attributeNames = [<string>]` . See <https://github.com/ScorpioBroker/ScorpioBroker/issues/381>
3. The datasource is stripping part of the path from the timeseries URL so we
   must append `ngsi-ld/v1` explicitly in the configuration

## Previous attempts at a mobility dashboard

Prior to the current grafana-based solution another attempt was made to use a
fiware-native dashboard <https://github.com/triveme/smartcity-dashboard> together
with QuantumLeap but the software worked under specific conditions that cannot
be met under the current technological stack. The experiment is archived in
commit d7b507e18c053f8aae25ac1cb3f1bf4cb8569a1d

## License

for the ODALA project.

© 2023 Phoops

License EUPL 1.2

![CEF Logo](https://ec.europa.eu/inea/sites/default/files/ceflogos/en_horizontal_cef_logo_2.png)

The contents of this publication are the sole responsibility of the authors and do not necessarily reflect the opinion of the European Union.
This project has received funding from the European Union’s “The Connecting Europe Facility (CEF) in Telecom” programme under Grant Agreement number: INEA/CEF/ICT/A2019/2063604
