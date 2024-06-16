# media-stack

A stack of self-hosted media managers and streamer without a VPN.

Stack include Radarr, Sonarr, Prowlarr, qBittorrent and Jellyfin.

## Coolify setup

Set domain names for each container to include ports:
qbittorrent:5080
prowlarr:3000
sonarr:3000
radarr:3000
jellyfin:8096

I also had to manually create a movies and shows folder within the download volume
```bash
sudo docker exec sonarr-INSERTID mkdir /downloads/movies
sudo docker exec sonarr-INSERTID mkdir /downloads/shows
sudo docker exec sonarr-INSERTID chown abc:users /downloads/movies
sudo docker exec sonarr-INSERTID chown abc:users /downloads/shows
```

## Requirements

- Docker version 24.0.5 and above
- Docker compose version v2.20.2 and above
- It may also work on some of lower versions, but its not tested.

## Docker setup

```
# create internal network, binds to localhost instead of 0.0.0.0
sudo docker network create internal -o "com.docker.network.bridge.host_binding_ipv4=127.0.0.1"
# create external network
sudo docker network create external
# start containers
sudo docker compose up -d
# get ssl certificate
sudo docker exec -it nginx ash
apk add certbot certbot-nginx
certbot certonly
# copy nginx config
sudo docker cp nginx.conf nginx:/etc/nginx/conf.d/default.conf
# reload nginx
sudo docker exec -it nginx nginx -s reload
```

## Namecheap Setup
|   Type   | Host | Value  |
|----------|------|--------|
| A Record | *    | ip     |
| A Record | @    | ip     |

Now configure radarr, sonarr, prowlarr, qbittorrent and jellyfin and enjoy 🏴‍☠️ .
