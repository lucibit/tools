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
              haugene/transmission-openvpn
```
`NOTE`
For NORDVPN you can no longer use your normal user/pass  See [here](https://support.nordvpn.com/General-info/1653315162/Changes-to-the-login-process-on-third-party-apps-and-routers.htm)

Also docker-compose version

```docker-compose
version: '3.3'
services:
    transmission-openvpn:
        cap_add:
            - NET_ADMIN
        volumes:
            - '/volume1/Media/Torrents/:/data'
            - '/volume1/docker/transmission/config/:/config'
        environment:
            - OPENVPN_PROVIDER=NORDVPN
            - OPENVPN_USERNAME=XXX
            - OPENVPN_PASSWORD=XXX
            - LOCAL_NETWORK=192.168.0.0/16
            - NORDVPN_PROTOCOL=tcp
            - NORDVPN_CATEGORY=legacy_p2p
            - NORDVPN_COUNTRY=NL
        logging:
            driver: json-file
            options:
                max-size: 10m
        ports:
            - '9091:9091'
        image: haugene/transmission-openvpn
```
