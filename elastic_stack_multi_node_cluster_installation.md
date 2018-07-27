# Elastic Stack multi-node cluster installation

Used this guide https://www.elastic.co/guide/en/elasticsearch/reference/6.3/rpm.html

```
yum install java-1.8.0-openjdk -y
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.2.rpm
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.2.rpm.sha512
shasum -a 512 -c elasticsearch-6.3.2.rpm.sha512
sudo rpm --install elasticsearch-6.3.2.rpm

systemctl daemon-reload
systemctl enable elasticsearch

cd /etc/elasticsearch
vim elasticsearch.yml

# Use a descriptive name for the node:
#
node.name: master1
node.data: false

# Set the bind address to a specific IP (IPv4 or IPv6):
#
network.host: ["localhost","172.31.30.184"]

systemctl start elasticsearch
systemctl status elasticsearch

```

Repeat the same steps for 2 more nodes.
