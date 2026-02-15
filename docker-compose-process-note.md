sudo yum install git -y
sudo yum install docker -y #linux 2023
sudo usermod -aG docker ec2-user
newgrp docker
sudo service docker start

FIX: Install Docker Compose v2 (Official Plugin)
Step 1: Create plugin directory
undefined

sudo mkdir -p /usr/libexec/docker/cli-plugins

Step 2: Download docker-compose plugin
undefined

sudo curl -SL https://github.com/docker/compose/releases/download/v2.27.0/docker-compose-linux-x86_64 \
-o /usr/libexec/docker/cli-plugins/docker-compose

Step 3: Make it executable
undefined

sudo chmod +x /usr/libexec/docker/cli-plugins/docker-compose

Step 4: Verify installation
undefined

docker compose version

👉 Output aise aayega:

undefined

Docker Compose version v2.27.0

⚡ Now Run Your Containers
undefined

docker compose up -d
