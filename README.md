# tools
Useful tools I make/pick up 

### Synology haugene/transmission-openvpn setup


```shell
sudo docker run --cap-add=NET_ADMIN -d \
              -v /volume1/Media/Torrents/:/data \
              -v /volume1/docker/transmission/config/:/config \
              -e OPENVPN_PROVIDER=NORDVPN \
              -e OPENVPN_USERNAME=XXXXXXX \
              -e OPENVPN_PASSWORD=XXXXXXX \
              -e NORDVPN_COUNTRY=NL \
              -e LOCAL_NETWORK=192.168.0.0/16 \
              --log-driver json-file \
              --log-opt max-size=10m \
              -p 9091:9091 \
              haugene/transmission-openvpn:4
```
