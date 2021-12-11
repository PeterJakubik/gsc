# Zobrazenie logov v elasticsearch
Adresár **atolog** obsahuje log data, ktoré chceme zobraziť v elasticu. 

Dáta obsahujú rýchlosť vlaku v `JSON` formáte
```json
 "v_TRAIN_ATO" : 14,
```

Vytvorením logstash konfiguráciu môžeme načítať dáta z logu a poslať ich do elasticu. Eleastic vloží rozparsované dáta do indexu.

## Čo treba nainštalovať
 * docker
 * logstash [logstash download](https://www.elastic.co/downloads/logstash).
    logstash treba rozbaliť do aktuálneho adresára `logstash`, tak aby sa dal spustiť `.\logstash\bin\logstash`

```
 │
 ├── [gsc]
 │    |
 │    └── [atologs]
 │        [logstash]
 │        .env
 │        README.md
 │        ...
```

## Component diagram
![Component Diagram](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/PeterJakubik/gsc/master/diagram.puml)

 
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

---
**NOTE**

Logstash sa distribuuje s javou, ak je na windows problém, treba pozrieť https://www.elastic.co/guide/en/logstash/current/running-logstash-windows.html 

---

 * V súbore `logstash.conf` treba nastaviť na riadku 4 absolútnu cestu k logom :-( 

```
 .\logstash\bin\logstash -f .\logstash.conf
```

