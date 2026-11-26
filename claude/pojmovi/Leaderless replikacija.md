---
tip: pojam
aliases: [leaderless replication, Dynamo-style replication]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Leaderless replication; Giuseppe DeCandia i drugi, Dynamo: Amazon's Highly Available Key-value Store, SOSP '07, 2007, odeljci 2.3 i 4.5, https://www.cs.purdue.edu/homes/bb/cs590/papers/amazon-dynamo-sosp2007.pdf"
---
# Leaderless replikacija (leaderless replication)

## Definicija

Leaderless replikacija jeste način replikacije u kome svaki [[Čvor replicirane baze|čvor replicirane baze]] može da primi upis direktno od klijenta, a klijent, ili koordinator u njegovo ime, šalje upis na više čvorova, pri čemu nijedan čvor ne nameće redosled upisa.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu bez čvora koji određuje redosled upisa, status poslovnog toka čuvaju N1, N2 i N3. N3 otkaže. Instanca servisa A šalje upis istovremeno na sva tri čvora, N1 i N2 ga primaju i potvrđuju, a instanca zanemaruje to što N3 nije odgovorio. Upis se smatra uspešnim ([[Kvorum#O kvorumu za čitanje i upis|kvorum]]). Otkaz N3 nije vidljiv iznad baze ([[Maskiranje otkaza|maskiranje otkaza]]). Kada se N3 vrati, nedostaje mu upis, koji se naknadno dopunjuje ([[Read repair]], [[Anti-entropy]]).

## Napomene

Razlika od [[Multi-leader replikacija|multi-leader replikacije]]: i tamo više čvorova prima upise, ali čvor koji je upis primio izmenu sam prosleđuje ostalima. Ovde upis na više čvorova šalje klijent ili koordinator, a koordinator ne nameće redosled upisa.

U primarnom kontekstu servisne instance upisuju samo na [[Primarni čvor|primarni čvor]] P, koji određuje redosled upisa, a posle njegovog otkaza upis se nastavlja tek posle [[Failover|failover-a]]. Leaderless replikacija nema ni P ni failover: otkaz jednog čvora ne zaustavlja upis dok ga potvrđuje dovoljan broj ostalih.

Čitanja se takođe šalju na više čvorova istovremeno, što omogućava da se otkriju čvorovi sa zastarelom vrednošću i da se vrednost popravi.

Bez lidera nema [[Izbor novog primarnog čvora|izbora novog primarnog čvora]], [[Fencing|fencing-a]] ni stanja [[Dva istovremena primarna čvora|dva istovremena primarna čvora]]. Istovremeni upisi istog podatka ipak mogu da stignu na različite čvorove, pa nastaje [[Sukob upisa|sukob upisa]], čak i kada se koristi kvorum.

Knjiga navodi da je model popularizovao Amazonov sistem Dynamo i da ga koriste Riak, Cassandra i Voldemort, zbog čega se naziva i Dynamo-style. U radu o Dynamo-u simetrija je izričito navedena kao princip: nijedan čvor nema posebne zadatke.
