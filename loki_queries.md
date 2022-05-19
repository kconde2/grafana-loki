# loki queries

```
{container="nginx"} |= "GET"
```

```
{job="adsb"} | json | gs > 500
```

```
sum by (query) (avg_over_time({job="dev/app"} |= "caller=metrics.go" | logfmt | duration > 100ms | unwrap througput_mb[1m]))
```

```
{job="dev/app"} |= "caller=metrics.go" | logfmt | throughput_mb < 100 and duration >= 200ms | line_format "{{.duration}}{{.query}}"
```
