# Loki

## Usage

```
make build
```

## Checks

http://localhost:3100/ready
http://localhost:3100/metrics


## GrafanaLoki Query

```json
{filename="/var/log/syslog",jobs="varlogs"} |= "docker"
```

## Docker Driver Client for Docker Logs scraping

Enable plugin

```shell
docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
```

Add the following configuration to `/etc/docker/daemon.json` [see details here](https://grafana.com/docs/loki/latest/clients/docker-driver/configuration/)

```json
{
    "debug": true,
    "log-driver": "loki",
    "logs-opts": {
        "loki-url": "http://localhost:3100/loki/api/v1/push",
        "loki-batch-size": "400"
    }
}
```

Run this to enable configurations

```shell
sudo systemctl restart docker
```

## References

- [Grafana Loki Configuration](https://grafana.com/docs/loki/latest/configuration/)
- [Collecting docker logs with loki 1](https://jlovec.net/2021/03/07/collecting-docker-logs-with-loki/)
- [Collecting docker logs with loki 2](https://linuxblog.xyz/posts/grafana-loki/)
- [Loki Queries](https://blog.ruanbekker.com/blog/2020/08/13/getting-started-on-logging-with-loki-using-docker/)
- [Configuration source](https://github.com/grafana/loki/tree/main/docs/sources)
