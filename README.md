# Monitoring dát v elasticsearch
Adresár **atolog** obsahuje log data, ktoré chceme zobraziť v elasticu. 

Dáta obsahujú rýchlosť vlaku v `JSON` formáte
```json
 "v_TRAIN_ATO" : 14,
```

Vytvorením logstash konfigurácie môžeme načítať dáta z logu a zapísať ich do elasticu. Eleastic vloží rozparsované dáta do indexu.
V kibane, môžeme potom dáta zobraziť

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
![Component Diagram](http://www.plantuml.com/plantuml/proxy?src=https://raw.githubusercontent.com/peterjakubik/gsc/master/diagram.puml)

 
## Spustenie elastiku a kibany v dockri
```bash
docker-compose up
```

Skontrolujeme či elastic beží
```bash
curl http://localhost:9200/_cluster/health?pretty

# Nody
curl http://localhost:9200/_cat/nodes?v
```

Kibana je dostupná na http://localhost:5601


## Logstash

---
**NOTE**

Logstash sa distribuuje s javou, ak je na windows problém, treba pozrieť https://www.elastic.co/guide/en/logstash/current/running-logstash-windows.html 

---

 * V súbore `logstash.conf` treba nastaviť na riadku 4 absolútnu cestu k logom :-( 

```
 .\logstash\bin\logstash -f .\logstash.conf
```

Logstash načíta dáta z logu, podľa pravidiel v súbore `logstash.conf` ich rozparsuje vrátane `JSON` dát a pošle ich do elastiku. 
Do elastiku sa posiela aj originál logu, aj rozparsované dáta, čo môže spôsobiť problém pri veľkom objeme dát (dá sa to vypnúť).

## Kibana
* Aby sme mohli v kibane pristupovať k dátam, treba vytvoriť **Index pattern**. Cez index pattern vieme pristúpiť k elasticsearch dátam.  
Vytvorenie index patternu v kibane:
1. _Discover_ ->  _Create index_
1. nastaviť meno indexu na **dev-ts*** 
1. nastaviť _Timestamp field_ na `@timestamp`
1. **Create index**

Dáta sú zo dňa 27.Nov.2021 tak treba v _Discover_ nastaviť časový filter tak aby sa zobrazili (last 30 days)
* parsed_json.v_TRAIN_ATO -> _Visualize_ -> Zmeniť typ grafu z 'Bar vertical' -> 'Line' -> _Save_
* parsed_json.v_TRAIN_ATO -> _Visualize_ -> _Median_ zmeniť na _Average_

## Bonus
Rado Ondas z ELastiku na https://radoondas.io/   
Napr. zobrazenie COVID dát https://radoondas.io/posts/2020/visualise-covid-19-using-elastic-stack/ 