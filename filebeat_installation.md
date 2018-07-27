# Filebeat installation and configuration

I got these steps from Linuxacademy.com with my minor modifications

```
mkdir /var/log/apache2
cd /var/log/apache2
wget https://github.com/smartrus/content-elastic-log-samples/raw/master/access.log

curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.3.2-x86_64.rpm
sudo rpm -vi filebeat-6.3.2-x86_64.rpm

systemctl enable filebeat

vi /etc/filebeat/filebeat.yml
filebeat setup
Loaded index template
Loading dashboards (Kibana must be running and reachable)
Exiting: Error importing Kibana dashboards: fail to create the Kibana loader: Error creating Kibana client: Error creating Kibana client: fail to get the Kibana version: HTTP GET request to /api/status fails: fail to execute the HTTP GET request: Get http://localhost:5601/api/status: dial tcp 127.0.0.1:5601: getsockopt: connection refused. Response: .


vi /etc/filebeat/filebeat.yml
# Change output to logstash


filebeat modules enable apache2

systemctl status logstash
systemctl status elasticsearch

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

systemctl start filebeat

tail /var/log/filebeat/filebeat

tail /var/lib/filebeat/registry
[{"source":"/var/log/apache2/access.log","offset":6,"timestamp":"2018-07-27T10:22:51.512147311Z","ttl":-1,"type":"log","meta":null,"FileStateOS":{"inode":22352675,"device":51713}}]

curl localhost:9200/_cluster/health?pretty=true
```
