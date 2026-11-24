---
tip: pojam
aliases: [shard map, request routing]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6, odeljak Request Routing, str. 214-216; Citus Documentation, Concepts, https://docs.citusdata.com/en/stable/get_started/concepts.html; MongoDB Manual, Config Servers, https://www.mongodb.com/docs/manual/core/sharded-cluster-config-servers/"
---
# Mapa šardova (shard map)

## Definicija

Mapa šardova jeste zapis o tome na kojim je čvorovima baze podataka smešten svaki [[Šard|šard]] i, ako se uloge tih čvorova razlikuju, koju ulogu koji čvor ima, na osnovu kojeg se zahtev upućuje čvoru koji može da ga izvrši.

## Primer

U primarnom cloud kontekstu, servis A upisuje korak toka 42. Iz [[Raspodela podataka po šardovima|raspodele]] sledi da tok pripada šardu S1, a iz mape da je primarni čvor tog šarda P1, pa usmerivač šalje upis na P1. Posle [[Failover|failover-a]] primarni čvor postaje R11. Usmerivač čija kopija mape još navodi P1 šalje upis pogrešnom čvoru.

## Napomene

Raspodela određuje kom šardu podatak pripada, a mapa gde je taj šard. Promena mape ne mora da promeni raspodelu.

Zastarela mapa je opasna ako stari primarni čvor i dalje prihvata upise, što sprečava [[Fencing]]. Ako se mapa čuva samo na jednom mestu, ona može biti [[Jedinstvena tačka otkaza|jedinstvena tačka otkaza]]: šardovi rade, ali zahtevi ne stižu do njih.
