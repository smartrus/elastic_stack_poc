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

Repeat the same steps for 2 more nodes (data1, data2) except the config in elasticsearch.yml.

```
# Use a descriptive name for the node:
#
node.name: data1
node.master: false

# Set the bind address to a specific IP (IPv4 or IPv6):
#
network.host: ["localhost","172.31.97.75"]

# Pass an initial list of hosts to perform discovery when new node is started:
# The default list of hosts is ["127.0.0.1", "[::1]"]
#
discovery.zen.ping.unicast.hosts: ["172.31.30.184"]

systemctl start elasticsearch
systemctl status elasticsearch
```

Diagnostic info about our cluster:

```
# check on each node
less /var/log/elasticsearch/elasticsearch.log

# check on master node
curl localhost:9200
{
  "name" : "master1",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "KQWYJucGT9mSz99kh791PQ",
  "version" : {
    "number" : "6.3.2",
    "build_flavor" : "default",
    "build_type" : "rpm",
    "build_hash" : "053779d",
    "build_date" : "2018-07-20T05:20:23.451332Z",
    "build_snapshot" : false,
    "lucene_version" : "7.3.1",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}

curl localhost:9200/_cluster/health?pretty=true
{
  "cluster_name" : "elasticsearch",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 3,
  "number_of_data_nodes" : 2,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100.0
}

```
