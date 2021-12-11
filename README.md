# Data v elasticsearch

## Čo treba nainštalovať
 * docker
 * logstash [logstash download](https://www.elastic.co/downloads/logstash)
   logstash treba rozbaliť do adresára `logstash`, tak aby sa dal spustiť `.\logstash\bin\logstash`

## Component diagram
![Component Diagram](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/PeterJakubik/gsc/master/UML/diagram.puml)

 
## Spustenie elastiku a kibany v dockri
```bash
docker-compose up
```

Skontrolujeme či elastic funguje
```bash
curl localhost:9200/_cluster/health?pretty
```

Kibana je dostupná na http://localhost:5601


# Logstash
 * V súbore `logstash.conf` treba nastaviť na riadku 4 absolútnu cestu k logom :-( 

```
 .\logstash\bin\logstash -f .\logstash.conf
```


# Ako to funguje
1. logstash nacita data z lokalneho suboru a posle do elastiku
1. kibana zobrazi data
