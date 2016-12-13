# Download ELK images

```
docker pull docker.io/logstash:latest
docker pull docker.io/elasticsearch:latest
docker pull docker.io/kibana:latest
```

# Configure logstash

Take elasticsearch as one of logstash output. Refer to etc/docker-elk/logstash/logstash.conf.
In production, I copy the logstash.conf to /etc/docker-elk/logstash/logstash.conf.

# Start ELK

start logstash

```
docker run -v /etc/docker-elk/logstash/logstash.conf:/config/logstash.conf \
           -p 5043:5043 -d --name my-logstash logstash:latest -f /config/logstash.conf
```

start elasticsearch

```
docker run -d --name my-elasticsearch -p 9200:9200 -v /var/esdata:/usr/share/elasticsearch/data elasticsearch:latest
```

start kibana 

```
docker run --link my-elasticsearch:elasticsearch -p 5601:5601 -d kibana
```

# Reference

https://hub.docker.com/_/logstash/
https://hub.docker.com/_/elasticsearch/
https://hub.docker.com/_/kibana/
