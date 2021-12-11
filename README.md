# Data v elasticsearch

## Čo treba nainštalovať
 * docker
 * logstash [logstash](https://www.elastic.co/downloads/logstash)
   * logstash bude priamo čítať log dáta z adresára. Reálne filebeat monitoruje dáta a posiela na logstash, ktorý beží spolu s elastikom

Logstash treba rozbalit v tom istom adresari ako repo.

## Spustenie elastiku a kibany v dockri
```bash
docker-compose up
```

Skontrolujeme ci elastic bezi
```bash
curl localhost:9200/_cluster/health?pretty
```

Kibana http://localhost:5601

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
```

# Logstash
 * Download logstash [download](https://www.elastic.co/downloads/logstash)
    Logstash na Windowse  distribuuje aj javu, ktoru potrebuje ako runtime https://www.elastic.co/guide/en/logstash/current/running-logstash-windows.html 

 * V súbore `logstash.conf` treba nastaviť na riadku 3 absolútnu cestu k logom :-( 

```
 .\logstash\bin\logstash -f .\logstash.conf
```


# Ako to funguje
1. logstash nacita data z lokalneho suboru a posle do elastiku
1. kibana zobrazi data
