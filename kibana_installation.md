# Kibana installation

```
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.3.2-x86_64.rpm
shasum -a 512 kibana-6.3.2-x86_64.rpm
sudo rpm --install kibana-6.3.2-x86_64.rpm

systemctl enable kibana

systemctl start kibana

tail -f /var/log/messages

ps -ef | grep kibana

ssh user@34.253.82.156 -L 5601:localhost:5601

```
