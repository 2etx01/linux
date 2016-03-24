# update
##chanege sources list

```
sed -i 's"http://mirrordirector.raspbian.org/raspbian/"http://free.nchc.org.tw/raspbian/raspbian/"' /etc/apt/sources.list
apt-get clean all
```

```
apt-get update
apt-get install raspi-config
```

use

```
raspi-config
```

expand filesystem and set up language

```
apt-get upgrade && apt-get dist-upgrade
```

## An easier way to update the firmware of your Raspberry Pi.

```
apt-get install rpi-update
rpi-update
```

##install zsh
```
apt-get install zsh git vim
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
chsh -s /bin/zsh
```


## use rpi-source
```
apt-get install make build-essential libncurses5-dev
sudo apt-get install python-pip
```
### install rpi-source
```
sudo wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/bin/rpi-source && sudo chmod +x /usr/bin/rpi-source && /usr/bin/rpi-source -q --tag-update

```
### install gcc
```
sudo wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/bin/rpi-source && sudo chmod +x /usr/bin/rpi-source && /usr/bin/rpi-source -q --tag-update
echo deb http://mirrordirector.raspbian.org/raspbian/ jessie main contrib non-free | sudo tee /etc/apt/sources.list.d/jessie.list
sudo apt-get update
sudo apt-get install -y gcc-4.8 g++-4.8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 20
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50
sudo rpi-source
```
