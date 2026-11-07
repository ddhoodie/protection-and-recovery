---
noteId: "49e0e9e0d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "failover initiation"
  - "failover trigger"
izvor: "Microsoft, Failover and failback, https://learn.microsoft.com/en-us/azure/reliability/concept-failover-failback"
---

# Pokretanje failover-a (failover initiation)

## Definicija

Pokretanje failover-a jeste odluka operatera ili automatske komponente da se na osnovu [[Otkrivanje otkaza primarnog čvora|otkrivenog otkaza primarnog čvora]] započne [[Failover|failover]].

## Primer

U primarnom cloud kontekstu, pravilo nadzorne komponente glasi da se failover pokreće ako primarni čvor P ne odgovara 10 sekundi i ako bar jedna replika potvrdi da ni ona ne prima poruke od njega. U 12:00:10 oba uslova su ispunjena i nadzorna komponenta pokreće failover bez čekanja operatera. Kraća granica, na primer 3 sekunde, ubrzala bi oporavak, ali bi kratkotrajno [[Usporavanje servisa|usporavanje]] čvora P moglo da pokrene nepotreban failover. Duža granica, na primer 2 minuta, smanjila bi taj rizik, ali bi potrošila petinu [[Ciljno vreme oporavka|RTO-a]] od 10 minuta pre nego što oporavak uopšte počne.

## Napomene

Pokretanje odvaja uslov za odluku od njenog izvršenja. Otkriven otkaz ne mora automatski voditi u failover, jer sistem može da sačeka dodatnu potvrdu ili odluku operatera.

Automatsko pokretanje je brže, ali se greška u pravilu ponavlja pri svakom otkazu bez ičije provere. Ručno pokretanje je sporije, ali operater može da uzme u obzir ono što pravilo ne vidi, na primer planirano održavanje ili šire smetnje u mreži. Zato se često kombinuju: jasni slučajevi se rešavaju automatski, a nejasni se prepuštaju operateru.

Uslovi za pokretanje mogu uključiti i proveru da postoji dovoljno ažurna replika. Ako nijedna replika nije dovoljno ažurna, failover bi doveo do gubitka podataka većeg od dozvoljenog po [[Ciljna tačka oporavka|RPO-u]], pa je bolje sačekati povratak čvora P. Odluka da se failover ne pokrene takođe je ishod ovog koraka. Pokretanje ne garantuje uspeh, jer i pokrenut failover može postati [[Neuspeli failover|neuspeli failover]].
