---
tip: pojam
aliases: [sloppy quorum]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Sloppy quorums and hinted handoff; Apache Cassandra Documentation, Hints, verzija 4.0, https://cassandra.apache.org/doc/4.0/cassandra/operating/hints.html; Giuseppe DeCandia i drugi, Dynamo: Amazon's Highly Available Key-value Store, SOSP '07, 2007, odeljak 4.6 Handling Failures: Hinted Handoff, https://www.cs.purdue.edu/homes/bb/cs590/papers/amazon-dynamo-sosp2007.pdf; Apache Cassandra Documentation, Dynamo, odeljak Tunable Consistency, https://cassandra.apache.org/doc/stable/cassandra/architecture/dynamo.html"
---
# Sloppy kvorum (sloppy quorum)

## Definicija

Sloppy kvorum jeste [[Kvorum#O kvorumu za čitanje i upis|kvorum]] koji, kada [[Čvor replicirane baze|čvorovi replicirane baze]] određeni da čuvaju podatak nisu dostupni, uračunava i potvrde čvorova izvan njih.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu bez čvora koji određuje redosled upisa, status poslovnog toka čuvaju N1, N2 i N3 (n = 3, w = 2, r = 2), a N4 nije određen da ga čuva. [[Prekid mreže|Prekid mreže]] između regija odvoji instancu servisa B u Regiji 2 od čvorova N1 i N2 u Regiji 1, a ona i dalje dosiže N3 i N4. Odgovori N1 i N2 ne stižu u okviru [[Rok čekanja|roka čekanja]], pa ih instanca smatra nedostupnim. Običan kvorum bi vratio grešku, jer je dostupan samo jedan određeni čvor. Sloppy kvorum prihvata upis, jer su ga potvrdili N3 i N4. N4 privremeno čuva izmenu uz hint da je namenjena čvoru N1. Čvor N2 nema zamenu, pa upis dobija tek popravkom ([[Read repair]] ili [[Anti-entropy]]). Kada se veza između regija vrati, N4 predaje izmenu čvoru N1. Do tada instanca u Regiji 1, koja dosiže N1 i N2, ali ne i N4, pri čitanju ne vidi upis, iako je w + r veće od n.

## Napomene

Sloppy kvorum povećava dostupnost upisa, jer upis uspeva čim w dostupnih čvorova potvrde upis, makar to nisu čvorovi koji ga inače čuvaju. Cena je što preklapanje skupova za upis i čitanje više nije zagarantovano. Prema knjizi to zapravo nije kvorum u uobičajenom smislu, već samo garancija trajnosti: podatak je sačuvan na w čvorova, ali čitanje ne mora da ga vidi dok hinted handoff nije završen. Zbog toga se običan kvorum, koji ostaje na određenim čvorovima, navodi kao suprotnost.

Hinted handoff je zaseban postupak: čvor izvan određenih privremeno čuva izmenu uz oznaku namenjenog čvora i predaje je tom čvoru kada postane dostupan. Sloppy kvorum određuje šta se računa kao uspešan upis, a hinted handoff šta se posle toga dešava sa izmenom. Sistemi ih koriste zajedno, ali ne moraju: Cassandra hint ne računa u potvrde, osim na nivou ANY.

Privremeno čuvana izmena može da se izgubi ako čvor koji je čuva otkaže pre predaje. Rad o Dynamo-u navodi da hinted handoff najbolje radi kada su otkazi privremeni, a za ostale slučajeve koristi [[Anti-entropy]].

Izbor između greške i prihvatanja upisa na drugom čvoru jeste oblik [[Kompromis konzistentnosti i dostupnosti tokom mrežne particije|kompromisa konzistentnosti i dostupnosti]]. U primarnom kontekstu, kada [[Mrežna particija|mrežna particija]] odvoji servis A od [[Primarni čvor|primarnog čvora]] P, upis ne može da se izvrši ni na jednom drugom čvoru dok se uloga ne prenese. Sloppy kvorum bira suprotno.

Prema knjizi, sloppy kvorum je opcion u uobičajenim Dynamo-style sistemima: neki ga imaju uključenog, a neki isključenog po podrazumevanim podešavanjima.
