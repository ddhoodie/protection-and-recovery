---
tip: pojam
aliases: [quorum, majority quorum, quorum reads and writes, read quorum, write quorum]
izvor: "David K. Gifford, Weighted Voting for Replicated Data, Proceedings of the 7th ACM Symposium on Operating Systems Principles (SOSP), 1979, str. 150–162, https://doi.org/10.1145/800215.806583; Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljci Quorums for reading and writing i Limitations of quorum consistency; Apache Cassandra Documentation, Dynamo, odeljak Tunable Consistency, https://cassandra.apache.org/doc/stable/cassandra/architecture/dynamo.html"
---

# Kvorum (quorum)

## Definicija

Kvorum jeste najmanji broj čvorova, među čvorovima koji čuvaju iste podatke ili zajedno donose istu odluku, čiji je odgovor ili pristanak dovoljan da se operacija ili odluka smatra važećom. Taj broj se bira tako da se skupovi čvorova čije se operacije ili odluke ne smeju mimoići preklapaju.

Dva uobičajena oblika su većinski kvorum, kojim se bira novi primarni čvor, i kvorum za čitanje i upis u leaderless replikaciji.

## Primer

### Većinski kvorum

U primarnom cloud kontekstu, čvorovi P, R1 i R2 nalaze se u tri različite zone dostupnosti, a za promenu primarnog čvora potreban je kvorum od dva čvora. Kada [[Mrežna particija|mrežna particija]] odvoji zonu 1, na jednoj strani je samo P, a na drugoj R1 i R2.

Strana sa R1 i R2 ima kvorum i može da izabere R1 za novi primarni čvor. Strana sa čvorom P nema kvorum i ne može da izabere novi primarni čvor.

Da su sva tri čvora u dve zone, na primer P i R1 u zoni 1, a R2 u zoni 2, odsecanje zone 1 ostavilo bi R2 bez kvoruma, pa bi otkaz jedne zone sprečio [[Failover|failover]].

### Kvorum za čitanje i upis

Ovaj oblik se prikazuje u sekundarnom kontekstu [[Cloud sistem u dve regije]], jer primarni kontekst ne može da ga predstavi: upise u njemu prima samo jedan čvor.

U modelu bez čvora koji određuje redosled upisa, status poslovnog toka čuvaju N1, N2 i N3 (n = 3). Upis zahteva dve potvrde (w = 2), a čitanje dva odgovora (r = 2).

N3 otkaže. Instanca servisa A šalje upis na sva tri [[Čvor replicirane baze|čvora replicirane baze]], N1 i N2 ga potvrđuju i upis je uspešan, iako ga N3 nije primio. Kada se N3 vrati, ima stariji status.

Instanca servisa B čita sa N2 i N3. N2 vraća noviji, a N3 stariji status. Pošto je w + r veće od n, skupovi čvorova za upis i za čitanje se preklapaju, u ovom slučaju u N2, pa instanca prepoznaje i uzima noviji status.

Da su otkazala dva čvora, ni upis ni čitanje ne bi dobili potrebna dva odgovora i vratili bi grešku.

## Napomene

### O većinskom kvorumu

Najčešći oblik je većinski kvorum: od n čvorova potrebno je više od polovine, odnosno ⌊n/2⌋ + 1. Svake dve većine imaju bar jedan zajednički čvor, pa u istom izboru ne mogu da postoje dve strane koje obe imaju kvorum. Zato se kod [[Izbor novog primarnog čvora|izbora novog primarnog čvora]] često koristi neparan broj učesnika, najmanje tri.

Kvorum štiti od dve nezavisne odluke, ali ne zaustavlja čvor koji je odluku doneo ranije. Stari [[Primarni čvor|primarni čvor]] na strani bez kvoruma i dalje može da prihvata upise ako ga nešto drugo ne zaustavi, na primer [[Zakup uloge primarnog čvora|zakup uloge]] ili [[Fencing|fencing]].

Strana bez kvoruma ne može da donese odluku za koju je kvorum potreban čak ni kada su svi njeni čvorovi ispravni. Kvorum zato povećava bezbednost podataka po cenu dostupnosti na manjinskoj strani, što je primena [[Kompromis konzistentnosti i dostupnosti tokom mrežne particije|kompromisa konzistentnosti i dostupnosti]].

### O kvorumu za čitanje i upis

Kod [[Leaderless replikacija|leaderless replikacije]] kvorum određuje koliko odgovora je potrebno za uspešan upis ili čitanje:

- n je broj čvorova predviđenih da čuvaju isti podatak;
- w je najmanji broj potvrda potrebnih za uspešan upis;
- r je najmanji broj odgovora potrebnih za čitanje.

Kada je w + r > n, svaki skup od w čvorova za upis i svaki skup od r čvorova za čitanje, izabranih među istih n čvorova, imaju bar jedan zajednički čvor. Time se omogućava da kasnije čitanje obuhvati bar jedan čvor koji je potvrdio prethodni uspešan upis.

Za n = 3 i w = r = 2 može se podneti otkaz jednog čvora, a za n = 5 i w = r = 3 otkaz dva čvora, pod uslovom da su preostali čvorovi dostupni i mogu da odgovore. Manji w i r povećavaju dostupnost uz veću verovatnoću zastarelih čitanja, što je takođe oblik [[Kompromis konzistentnosti i dostupnosti tokom mrežne particije|kompromisa konzistentnosti i dostupnosti]].

Kvorum za upis i kvorum za čitanje ne moraju biti većina. Na primer, moguće je podesiti w = n i r = 1. U dokumentaciji Cassandra-e naziv QUORUM označava većinu replika, što je jedan od mogućih nivoa konzistentnosti.

Preklapanje ne garantuje najnoviju vrednost u svim okolnostima. Knjiga navodi izuzetke, između ostalog [[Sloppy kvorum|sloppy kvorum]], [[Istovremenost upisa|istovremene upise]], upis koji je uspeo na manje od w čvorova i nije poništen, i obnovu čvora iz starije kopije. Zato ispunjen uslov preklapanja ne daje zagarantovanu jaku konzistentnost ([[CAP teorema|CAP teorema]]).

Uslov preklapanja potiče iz Giffordovog rada o glasanju za replicirane podatke, u kome se za čitanje i upis moraju sakupiti dovoljni brojevi glasova, tako da je njihov zbir veći od ukupnog broja glasova.

U primarnom kontekstu upis potvrđuje [[Primarni čvor|primarni čvor]]. Kod sinhrone replikacije on pre toga čeka potvrdu replika od kojih se to zahteva ([[Replikacija podataka sa primarnog čvora na replike|replikacija]]), pa broj potrebnih čvorova određuje jedan čvor. Kod kvoruma za čitanje i upis broj potvrda prati klijent, ili koordinator u njegovo ime.

Beleška [[Konzistentnost podataka]] meri zaostajanje prema izmenama koje je potvrdio primarni čvor. U leaderless replikaciji takvog čvora nema, pa se zaostajanje određuje prema poslednjem uspešnom upisu.
