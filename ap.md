
# wireless

```
apt-get install wireless-tools usbutils
```
## install hostapd
```
apt-get install hostapd
sudo apt-get remove hostapd
```

**download RTL8188C**

URL : <https://github.com/wxjeacen/RTL8188C>


**make hostapd**

```
cd wpa_supplicant_hostapd/wpa_supplicant_hostapd-0.8/hostapd
make clean
make
make install
```

```
sudo cp /usr/local/bin/* /usr/sbin/
```

**make wireless_tools**

```
cd /home/pi/RTL8188C/wireless_tools/
tar zxvf  wireless_tools.30.rtl.tar.gz
cd wireless_tools.30.rtl
make clean
make
make install
```
**vim /etc/hostapd/hostapd.conf**

```
interface=wlan0
driver=rtl871xdrv
#wifi 名稱
ssid=櫻桃
# 無線網絡的制式802.11g
hw_mode=g
channel=3
# 認證算法 1=OSA, 2=SKA, 3=both
auth_algs=1
# 連接方式爲wpa/wpa2
wpa=3
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP
rsn_pairwise=CCMP
#WiFi密碼
wpa_passphrase=12345678
#802.11n
wme_enabled=1
ieee80211n=1
ht_capab=[HT40+][SHORT-GI-40][DSSS_CCK-40]
```

**autostart hostapd**

vim /etc/default/hostapd

```
RUN_DAEMON=”yes”
DAEMON_CONF=”/etc/hostapd/hostapd.conf”
```

## interfaces

**vim /etc/network/interfaces**

```
auto wlan0
iface wlan0 inet static
address 192.168.1.1 
netmask 255.255.255.0
```
## DNS
**install**

```
apt-get install dnsmasq
```

**vim /etc/dnsmasq.conf**

```
vim /etc/dnsmasq.conf 

interface=wlan0
dhcp-range=192.168.1.2,192.168.1.127,12h
```

**autostart**

vim /etc/default/dnsmasq

```
DNSMASQ_OPTS="--conf-file=/etc/dnsmasq.conf"
#CONFIG_DIR=/etc/dnsmasq.d
```
```
/etc/init.d/dnsmasq restart
```
## Iptables
**install**

```
apt-get install iptables-persistent
```

**rule**

```
sysctl net.ipv4.ip_forward=1
iptables -A INPUT -i wlan0 -j ACCEPT
iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE
```

**autostart**

```
cp ap.sh /etc/init.d
update-rc.d ap.sh defaults
```