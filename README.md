# selfhosted

These are services I self-host on my local network.

## Services

* [mealie](https://mealie.io) - recipe tracker
* [paperless](https://docs.paperless-ngx.com) - document manager
* [uptime-kuma](https://github.com/louislam/uptime-kuma) - health monitor for my other services

## Backup

TODO: setup automatic volume backup with [docker-volume-backup](https://github.com/offen/docker-volume-backup#recurring-backups-in-a-compose-setup)

## Notes to self

To copy data from one volume to another, use the following command:

```bash
docker run --rm -it -v uptime-kuma:/from -v uptime-kuma_uptime-kuma:/to alpine ash -c "cd /from ; cp -av . /to"
```
