# Logstash installation and pipeline configuration

Logstash installation from rpm

```
wget https://artifacts.elastic.co/downloads/logstash/logstash-6.2.3.rpm
rpm --install logstash-6.2.3.rpm

systemctl enable logstash

ls -la /etc/logstash/
total 40
drwxr-xr-x.   3 root root 4096 Jul 27 09:40 .
drwxr-xr-x. 109 root root 8192 Jul 27 09:39 ..
drwxrwxr-x.   2 root root    6 Mar 13 11:55 conf.d
-rw-r--r--.   1 root root 1738 Mar 13 11:55 jvm.options
-rw-r--r--.   1 root root 1334 Mar 13 11:55 log4j2.properties
-rw-r--r--.   1 root root 6378 Jul 27 09:40 logstash.yml
-rw-r--r--.   1 root root  285 Mar 13 11:55 pipelines.yml
-rw-------.   1 root root 1659 Mar 13 11:55 startup.options

cd /etc/logstash/conf.d
wget https://github.com/smartrus/content-elastic-log-samples/raw/master/apache.conf

systemctl start logstash
systemctl status logstash
```
