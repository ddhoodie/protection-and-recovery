---
tip: pojam
aliases: [hot spot, hot shard]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6, str. 201 i odeljak Skewed Workloads and Relieving Hot Spots, str. 205; Microsoft, Azure Architecture Center, Sharding pattern, https://learn.microsoft.com/en-us/azure/architecture/patterns/sharding"
---
# Nesrazmerno opterećen šard (hot spot)

## Definicija

Nesrazmerno opterećen šard jeste [[Šard|šard]] koji prima znatno veći deo zahteva nego ostali šardovi iste baze podataka.

## Primer

U primarnom cloud kontekstu, tok 42 upisuje hiljade koraka u sekundi, dok ostali tokovi upisuju po nekoliko. Svi njegovi koraci pripadaju šardu S1, pa P1 odgovara sporo, a P2 i P3 su skoro neopterećeni. Pokretanje [[Failover|failover-a]] na R11 ne pomaže, jer isti zahtevi zatim stižu na R11.

## Napomene

Spor odgovor takvog šarda može se pogrešno protumačiti kao otkaz pri [[Detekcija otkaza|detekciji otkaza]].

Raspodela po hešu ne pomaže kada zahtevi ciljaju istu vrednost [[Ključ šardovanja|ključa šardovanja]]. Dodavanje slučajnog broja ključu raspoređuje upise na više šardova, ali čitanje mora da spoji podatke iz svih njih.
