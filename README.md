# selfhosted

These are services I self-host on my local network.

## Services

* [paperless](https://docs.paperless-ngx.com) - document manager
* [uptime-kuma](https://github.com/louislam/uptime-kuma) - health monitor for my other services
* [Nginx Proxy Manager](https://nginxproxymanager.com) - proxy hosts to different services
* [Starbase 80](https://github.com/notclickable-jordan/starbase-80) - a nice dashboard
* [Whisper ASR](https://github.com/ahmetoner/whisper-asr-webservice/) - API server to access Whisper model
* [Ollama](https://ollama.ai) - API server to access open-source LLM models

## Backup

Automatic backups are handled with [docker-volume-backup](https://github.com/offen/docker-volume-backup#recurring-backups-in-a-compose-setup)

## Notes to self

To copy data from one volume to another, use the following command:

```bash
docker run --rm -it -v uptime-kuma:/from -v uptime-kuma_uptime-kuma:/to alpine ash -c "cd /from ; cp -av . /to"
```

To update an image, we must first delete the local image or hard-code the image version:

```bash
docker-compose down -rmi all
docker-compose up -d
```

To load TS script:

```bash
cp gg.neil.ts.plist ~/Library/LaunchAgents/gg.neil.ts.plist
launchctl load ~/Library/LaunchAgents/gg.neil.ts.plist
launchctl list | grep gg.neil
```

The last command confirms it is correctly loaded and running

### Ollama setup

After downloading Ollama, download your preferred model (currently I use mistral with my 8gb of VRAM):

```bash
ollama pull mistral
```

Also configure remote access to the server (safe to do only because my machine is not public-facing):

```bash
launchctl setenv OLLAMA_HOST "0.0.0.0"
launchctl setenv OLLAMA_ORIGINS "*"
```

Then restart ollama.
