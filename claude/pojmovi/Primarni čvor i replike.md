---
tip: pojam
aliases: [primary node and replicas, leader-based replication]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Leaders and Followers"
---
# Primarni čvor i replike (primary node and replicas)

## Definicija

Primarni čvor i replike jesu raspored čvorova baze podataka u kojem jedan [[Primarni čvor|primarni čvor]] prima i izvršava zahteve za izmenu podataka, a jedna ili više [[Replika|replika]] održava kopije njegovih podataka.

## Primer

U primarnom cloud kontekstu, baza ima jedan primarni čvor i više replika. Servisne instance upisuju podatke samo na primarni čvor, a izmene sa njega stižu do replika, a ne obrnuto. Primarni čvor periodično šalje [[Signal života|signal života]] replikama, na osnovu kojeg replika procenjuje da li se on i dalje izvršava.

## Napomene

Raspored pretpostavlja da u jednom trenutku postoji najviše jedan primarni čvor, jer samo tada sve izmene prolaze kroz jedno mesto i replike imaju jedinstven izvor izmena. Ako bi dva čvora istovremeno primala i izvršavala zahteve za izmenu, njihovi podaci bi se mogli razići, a to više ne bi bio ovaj raspored.

Sam raspored ne određuje šta se dešava kada primarni čvor otkaže: replike čuvaju kopije podataka, ali nastavak upisa zahteva da neki čvor preuzme ulogu primarnog.

Kako izmene stižu do replika opisuje [[Replikacija podataka sa primarnog čvora na replike]], a šta čitanje sa replike vraća u odnosu na potvrđene izmene opisuje [[Konzistentnost podataka]].
