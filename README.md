# v2ray-reality-dockercompose

# Requirements
* Update v2ray client: https://github.com/2dust/v2rayN/releases

# Initilization
```
xray_image="teddysun/xray:1.8.1"
key_pair=$(sudo docker run --rm ${xray_image} xray x25519)

PUBLIC_IP=$(curl -s ipv4.wtfismyip.com/text)

UPSTREAM_UUID=$(cat /proc/sys/kernel/random/uuid)
BRIDGE_UUID=$(cat /proc/sys/kernel/random/uuid)
PUBLIC_KEY=$(echo "${key_pair}"|grep -oP '(?<=Public key: ).*')
PRIVATE_KEY=$(echo "${key_pair}"|grep -oP '(?<=Private key: ).*')
SNIPORT_IRANCELL=www.google-analytics.com:443
SNI_IRANCELL=www.google-analytics.com
SNIPORT_MCI=www.googletagmanager.com:443
SNI_MCI=www.googletagmanager.com

## Fill xray.conf files using these values

# Create client configs (Don't forget to replace variables (UPSTREAM_IP and BRIDGE_IP))
client_config_bride_irancell="vless://${UUID}@${BRIDGE_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_IRANCELL}#Reality-Bridge-1"
client_config_bride_mci="vless://${UUID}@${BRIDGE_IP}:8443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_IRANCELL}#Reality-Bridge-2"
client_config_upstream_irancell="vless://${UUID}@${UPSTREAM_IP}:443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_IRANCELL}#Reality-Upstream-1"
client_config_upstream_mci="vless://${UUID}@${UPSTREAM_IP}:8443?security=reality&encryption=none&pbk=${PUBLIC_KEY}&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision&sni=${SNI_IRANCELL}#Reality-Upstream-2"
echo ""
echo "=================================================="
echo "Client configs:"
echo ""
echo "$client_config_bride_irancell"
qrencode -t ansiutf8 "${client_config_bride_irancell}"
echo ""
echo "$client_config_bride_mci"
qrencode -t ansiutf8 "${client_config_bride_mci}"
echo ""
echo "$client_config_upstream_irancell"
qrencode -t ansiutf8 "${client_config_upstream_irancell}"
echo ""
echo "$client_config_upstream_mci"
qrencode -t ansiutf8 "${client_config_upstream_mci}"
```

## Todo
* Automate variable initializations : ``` cat xray.conf.tmpl | evnsubst > xray.conf ```
* Add **BBR**
* Investigate MCI,Irancell, and other networks

# Links
https://raw.githubusercontent.com/mack-a/v2ray-agent/master/install.sh

https://github.com/miladrahimi/v2ray-docker-compose/

https://telegra.ph/How-run-Reality-protocol-with-Xray-or-Sing-box-Core-with-iSegaro-04-18

https://github.com/XTLS/RealiTLScanner