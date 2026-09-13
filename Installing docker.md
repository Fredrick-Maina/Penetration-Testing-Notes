sudo apt update
sudo apt install -y docker.io

sudo systemctl start docker
sudo systemctl enable docker

docker --version # check version

sudo docker run hello-world

# add user to docker Group
sudo usermod -aG docker $USER

newgrp docker

groups # verify

docker run hello-world # test without sudo

mkdir analysis folder

cd 

cp file into it

# run docker container

docker run -it --name file_sandbox ubuntu:20.04 bash

# inside container
apt update
apt install -y strace ltrace file netcat gdb
exit

# Copy the beacon file
docker cp ~/beacon_analysis/beacon.bin beacon_sandbox:/tmp/beacon.bin

# Remove old container if it exists
docker rm beacon_sandbox 2>/dev/null

# Run with full security
docker run -it --rm \
  --name beacon_sandbox \
  --network none \
  --read-only \
  --tmpfs /tmp \
  --user nobody \
  --cap-drop ALL \
  ubuntu:20.04 bash
  
docker cp ~/beacon_analysis/beacon.bin beacon_sandbox:/tmp/beacon.bin

# Go to /tmp
cd /tmp

# Check file
ls -la
file beacon.bin

# Make executable
chmod +x beacon.bin

# Run with strace to monitor
strace -f -e trace=network,file,process ./beacon.bin