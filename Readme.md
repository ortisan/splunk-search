#Splunk Searching

```sh
docker run -p 8000:8000 -e "SPLUNK_START_ARGS=--accept-license" -e "SPLUNK_PASSWORD=p@ssw0rd" --name splunk splunk/splunk:latest
```

#### Search

1. Calcula o tempo médio entre os eventos e gráfico por minuto:

```sh
source="log4j-application.log" sourcetype="log4j-test" | sort _time | streamstats window=1 current=f values(_time) as prev_time | eval diff_time = _time - prev_time | timechart span=1m eval(avg(diff_time)) BY sourcetype
```
