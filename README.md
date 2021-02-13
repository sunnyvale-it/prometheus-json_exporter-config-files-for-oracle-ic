# Prometheus json_exporter config files for consuming Oracle Integration Cloud REST APIs

A **[prometheus-community/json_exporter](https://github.com/prometheus-community/json_exporter)** config file to export metrics from **[Oracle Integration Cloud](https://www.oracle.com/it/integration/)** **[REST APIs](https://docs.oracle.com/en/cloud/paas/integration-cloud/rest-api)** in Prometheus text-based metric format. 

Before start, open the config file and set a valid username and password to let the json exporter connect to your OIC instance

```console
$ cat config.yaml
...
    basic_auth:
     username: myuser
     password: mysupersecretpassword
...
```

Clone the **[prometheus-community/json_exporter](https://github.com/prometheus-community/json_exporter)** GitHub repo

```console
$ git clone https://github.com/prometheus-community/json_exporter.git
```

Compile the source code 

```console
$ cd json_exporter && make ; cd ..
```

Run the exporter using one of the config files you get from this repo (metrics by default will be availanle at HTTP port 7979)

```console
$ ./json_exporter/json_exporter --web.listen-address=":7979" --config.file config_errors.yaml &
```

Test it by scraping metrics (remember to change the placeholder **\<MY OIC INSTANCE\>** accordingly)

```console
$ curl "http://localhost:7979/probe?target=https://<MY OIC INSTANCE>.integration.ocp.oraclecloud.com:443/ic/api/integration/v1/monitoring/errors"
# HELP errored_instances_in_the_past_hour_count Retrieves information about all integration instances that have a errored status in the past hour (https://docs.oracle.com/en/cloud/paas/integration-cloud/rest-api/op-ic-api-integration-v1-monitoring-errors-get.html)
# TYPE errored_instances_in_the_past_hour_count untyped
errored_instances_in_the_past_hour_count 0
```


