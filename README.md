# v2ray-reality-dockercompose

xray_image="teddysun/xray:1.8.1"
key_pair=$(sudo docker run --rm ${xray_image} xray x25519)
UUID=$(cat /proc/sys/kernel/random/uuid)
PUBLIC_KEY=$(echo "${key_pair}"|grep -oP '(?<=Public key: ).*')
PRIVATE_KEY=$(echo "${key_pair}"|grep -oP '(?<=Private key: ).*')
SHORT_ID=$(openssl rand -hex 8)
SNIPORT_IRANCELL=www.google-analytics.com:443
SNI_IRANCELL=www.google-analytics.com
SNIPORT_MCI=www.googletagmanager.com:443
SNI_MCI=www.googletagmanager.com

client_config_irancell="vless://[UUID]@[PUBLIC_IP]:443?security=reality&encryption=none&alpn=h2,http/1.1&pbk=[PUBLIC_KEY]&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision-udp443&sni=[DOMAIN]&sid=[SHORT_ID]#Reality-Irancell"
client_config_irancell="vless://[UUID]@[PUBLIC_IP]:8443?security=reality&encryption=none&alpn=h2,http/1.1&pbk=[PUBLIC_KEY]&headerType=none&fp=chrome&type=tcp&flow=xtls-rprx-vision-udp443&sni=[DOMAIN]&sid=[SHORT_ID]#Reality-MCI"
echo ""
echo "=================================================="
echo "Client configuration:"
echo ""
echo "$client_config"
echo ""
echo "Or you can scan the QR code:"
echo ""
qrencode -t ansiutf8 "${client_config}"


cat xray.conf.tmpl | evnsubst > xray.conf