# v2ray-reality-dockercompose

# Requirements
* Update V2ray client: https://github.com/2dust/v2rayNG/releases to support *Reality*
* Require *Docker* and *Docker Compose* installed on servers

# Initilization
```

# Run these commands on any system that has docker installed


export BRIDGE_IP=""
export UPSTREAM_IP=""

xray_image="teddysun/xray:1.8.1"
key_pair=$(sudo docker run --rm ${xray_image} xray x25519)
git clone https://github.com/hadi2f244/v2ray-reality-dockercompose && cd v2ray-reality-dockercompose
export BRIDGE_UUID=$(cat /proc/sys/kernel/random/uuid)
export UPSTREAM_UUID=$(cat /proc/sys/kernel/random/uuid)
export PRIVATE_KEY=$(echo "${key_pair}"|grep -oP '(?<=Private key: ).*')
export PUBLIC_KEY=$(echo "${key_pair}"|grep -oP '(?<=Public key: ).*')
export SNIPORT_IRANCELL=www.google-analytics.com:443
export SNI_IRANCELL=www.google-analytics.com
export SNIPORT_MCI=www.googletagmanager.com:443
export SNI_MCI=www.googletagmanager.com
echo ""
echo "BRIDGE_UUID: $BRIDGE_UUID"
echo "UPSTREAM_UUID: $UPSTREAM_UUID"
echo "PRIVATE_KEY: $PRIVATE_KEY"
echo "PUBLIC_KEY: $PUBLIC_KEY"
echo "SNIPORT_IRANCELL: $SNIPORT_IRANCELL"
echo "SNI_IRANCELL: $SNI_IRANCELL"
echo "SNIPORT_MCI: $SNIPORT_MCI"
echo "SNI_MCI: $SNI_MCI"

## Fill xray.conf files using these values Or you can use these scripts as well
cp v2ray-reality-bridge/xray_bridge.conf v2ray-reality-bridge/xray_bridge.conf.tmpl && envsubst < v2ray-reality-bridge/xray_bridge.conf.tmpl > v2ray-reality-bridge/xray.conf
cp v2ray-reality-upstream/xray_upstream.conf v2ray-reality-upstream/xray_upstream.conf.tmpl && envsubst < v2ray-reality-upstream/xray_upstream.conf.tmpl > v2ray-reality-upstream/xray.conf

# Create client configs (Don't forget to replace variables (UPSTREAM_IP and BRIDGE_IP))


############

client_config_upstream_irancell="vless://${UPSTREAM_UUID}@${UPSTREAM_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_IRANCELL}#Reality-Upstream-Irancell"

client_config_upstream_grpc_irancell="vless://${UPSTREAM_UUID}@${UPSTREAM_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=grpc&serviceName=grpc&sni=${SNI_IRANCELL}#Reality-Upstream-Irancell-grpc"

client_config_upstream_mci="vless://${UPSTREAM_UUID}@${UPSTREAM_IP}:8443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_MCI}#Reality-Upstream-Mci"

client_config_bridge_irancell="vless://${BRIDGE_UUID}@${BRIDGE_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_IRANCELL}#Reality-Bridge-Irancell"

client_config_bridge_grpc_irancell="vless://${BRIDGE_UUID}@${BRIDGE_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=grpc&serviceName=grpc&sni=${SNI_IRANCELL}#Reality-Bridge-Irancell-grpc"

client_config_bridge_mci="vless://${BRIDGE_UUID}@${BRIDGE_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_MCI}#Reality-Bridge-Mci"

echo ""
echo "=================================================="
echo "Client configs:"
echo ""
echo "$client_config_upstream_irancell"
qrencode -t ansiutf8 "${client_config_upstream_irancell}"
echo ""
echo "$client_config_upstream_grpc_irancell"
qrencode -t ansiutf8 "${client_config_upstream_grpc_irancell}"
echo ""
echo "$client_config_upstream_mci"
qrencode -t ansiutf8 "${client_config_upstream_mci}"
echo ""
echo "$client_config_bridge_irancell"
qrencode -t ansiutf8 "${client_config_bridge_irancell}"
echo ""
echo "$client_config_bridge_grpc_irancell"
qrencode -t ansiutf8 "${client_config_bridge_grpc_irancell}"
echo ""
echo "$client_config_bridge_mci"
qrencode -t ansiutf8 "${client_config_bridge_mci}"
echo ""
```


# Notes:
* It seems Irancell and MCI configs are not working on some IPs
* grpc configs sometimes works better that simple reality


## Todo
* Automate variable initializations : ``` cat xray.conf.tmpl | evnsubst > xray.conf ```
* Add **BBR**
* Investigate MCI,Irancell, and other networks
* Use two different public/private keys for upstream and bridge
* Connection between upstream and bridge can be other than just Reality that may make connection better
* Better Dns

# Links
https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh

https://github.com/miladrahimi/v2ray-docker-compose/

https://telegra.ph/How-run-Reality-protocol-with-Xray-or-Sing-box-Core-with-iSegaro-04-18

https://github.com/XTLS/RealiTLScanner

https://github.com/SasukeFreestyle/XTLS-Iran-Reality

https://github.com/sajjaddg/xray-reality

https://twitter.com/iSegaro
