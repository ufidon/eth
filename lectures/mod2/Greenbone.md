# Run Greenbone OpenVAS on WSL2 Ubuntu

## Install Docker Engine on Ubuntu

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get install     ca-certificates     curl     gnupg     lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo docker run hello-world # failed due to nftables used instead of iptables

# !!!
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy

# run docker without sudo
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker

# enable systemctl
# create and put the following two lines in /etc/wsl.conf
[boot]
systemd=true

# run docker at system startup
sudo systemctl enable docker.service
sudo systemctl enable containerd.service


# greenbone docker container
sudo apt install curl
sudo apt install python3 python3-pip
python3 -m pip install --user docker-compose

# append the following line to ~/.bashrc
export PATH="$PATH:/home/$USER/.local/bin/docker-compose"

# Create download directory
export DOWNLOAD_DIR=$HOME/greenbone-community-container && mkdir -p $DOWNLOAD_DIR

# Downloading docker-compose file
cd $DOWNLOAD_DIR && curl -f -L https://greenbone.github.io/docs/latest/_static/docker-compose-22.4.yml -o docker-compose.yml

# Downloading the Greenbone Community Containers
docker-compose -f $DOWNLOAD_DIR/docker-compose.yml -p greenbone-community-edition pull

# Starting the Greenbone Community Containers
# By default, a user admin with the password admin is created
docker-compose -f $DOWNLOAD_DIR/docker-compose.yml -p greenbone-community-edition up -d

# Updating password of administrator user
docker-compose -f $DOWNLOAD_DIR/docker-compose.yml -p greenbone-community-edition \
    exec -u gvmd gvmd gvmd --user=admin --new-password=<password>

# Opening Greenbone Security Assistant in the browser
xdg-open "http://127.0.0.1:9392" 2>/dev/null >/dev/null &  
```

* [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
  * [Docker Engine post-installation steps](https://docs.docker.com/engine/install/linux-postinstall/)
* [Solving Native Docker (Not Docker Desktop) unable to start on Ubuntu 20.10+ on WSL](https://patrickwu.space/2021/03/09/wsl-solution-to-native-docker-daemon-not-starting/)
* [Systemd support is now available in WSL!](https://devblogs.microsoft.com/commandline/systemd-support-is-now-available-in-wsl/)
* [Greenbone Community Containers](https://greenbone.github.io/docs/latest/22.4/container/index.html)