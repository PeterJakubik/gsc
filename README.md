# Data v elasticsearch

## Čo treba nainštalovať
 * docker
 * logstash [logstash download](https://www.elastic.co/downloads/logstash)
   logstash treba rozbaliť do adresára `logstash`, tak aby sa dal spustiť `.\logstash\bin\logstash`

 
## Spustenie elastiku a kibany v dockri
```bash
docker-compose up
```

Skontrolujeme či elastic funguje
```bash
curl localhost:9200/_cluster/health?pretty
```

Kibana je dostupná na http://localhost:5601

```plantuml
@startuml

package "Elastic + kibana" {
    API(9200) - [Elasticsearch]
    API(5601) - [Kibana]
}

package "Logstash" {
 [logstash]
}

folder "atologs" {
  [ob.log]
}

 [logstash] --> [ob.log]
 [Elasticsearch] --> [logstash]
 
 @enduml
```

# Logstash
 * V súbore `logstash.conf` treba nastaviť na riadku 4 absolútnu cestu k logom :-( 

```
 .\logstash\bin\logstash -f .\logstash.conf
```


# Ako to funguje
1. logstash nacita data z lokalneho suboru a posle do elastiku
1. kibana zobrazi data
