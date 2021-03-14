# Grafana Dashboard
I used this [dashboard](https://grafana.com/grafana/dashboards/12428) of [Derek-K](https://github.com/Derek-K/telegraf-speedtest) to keep checking my network with Speedtest and show it with Grafana

## Techs
- [Speedtest - CLI](https://www.speedtest.net/pt/apps/cli) - to test internet bandwidth
- [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/) - to collect the metrics and send to InfluxDB
- [InfluxDB](https://www.influxdata.com/) - A database for time series data
- [Grafana](https://grafana.com/) - To present the data

## First access
- Before run `speedtest-telegraf`, run `speedtest-influxdb` to initialize the InfluxDB and allow telegraf to create the database 
- Then up the rest 
- After `speedtest-telegraf` is up, you should run `speedtest` CLI for the first time by your hand to accept the license agreement
1. open container terminal `docker exec -it speedtest-telegraf /bin/bash`
2. execute `/speedtest/speedtest`
3. Answer YES for all

- The last, configure the Datasource and Dashboard on Grafana

## Datasource 
- Menu > Configuration > Datasource
- Click on `Add data source`
- Find for `InfluxDB`
- Running with this docker configuration. fill the fields with:
    - url: `http://speedtest-influxdb:8086`
    - basic auth: `check`
    - with credentials: `check`
    - On basic Auth Details, user & password is: `admin`
    - database: `Speedtest`
    - user & admin: `admin`
    - Finally: `Save and Test`

## Dashboard
- Menu > Dashboard > Manage > Import
- Import via granafa.com: `12428` 

## Environment Variable
 - GF_SERVER_DOMAIN: This environment tells to grafana which is the server domain, when the alerts runs on your notification channel, this will send `URL: SERVER_DOMAIN` in the notification's body.

Thanks to [Derek-K](https://github.com/Derek-K/telegraf-speedtest)