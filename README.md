## Instalacao de driver de rede Motorcomm YT6801 no mini pc MLLSE N3350 6GB RAM utilizando UBUNTU SERVER 24.04

# Instalação do driver

sudo apt update

sudo apt install build-essential

git clone https://github.com/rafaelbergo/driver-motorcomm-YT6801.git

sudo apt install build-essential

sudo su

cd src/

./yt_nic_install.sh

# Configuração da interface de rede

cd /etc/netplan/

sudo vim 50-cloud-init.yaml

adicionar no arquivo:

```
# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    version: 2
    ethernets:
        eno1:
            dhcp4: false
            dhcp6: false
            addresses:
                - 192.168.1.27/24
            routes:
                - to: default
                  via: 192.168.1.1
            nameservers:
                addresses:
                    - 1.1.1.1
                    - 1.0.0.1
```

sudo netplan apply

