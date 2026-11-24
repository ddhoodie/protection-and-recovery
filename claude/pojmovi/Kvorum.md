---
tip: pojam
aliases: [quorum, majority quorum]
izvor: "David K. Gifford, Weighted Voting for Replicated Data, Proceedings of the 7th ACM Symposium on Operating Systems Principles (SOSP), 1979, str. 150-162"
---
# Kvorum (quorum)

## Definicija

Kvorum jeste najmanji broj čvorova, među čvorovima koji čuvaju iste podatke ili zajedno donose istu odluku, čiji je odgovor ili pristanak dovoljan da se operacija ili odluka smatra važećom. Taj broj se bira tako da svaka dva skupa čvorova čije se operacije ili odluke ne smeju mimoići imaju bar jedan zajednički čvor.

## Primer

U primarnom cloud kontekstu, čvorovi P, R1 i R2 nalaze se u tri različite zone dostupnosti, a za promenu primarnog čvora potreban je kvorum od dva čvora. Kada [[Mrežna particija|mrežna particija]] odvoji zonu 1, na jednoj strani je samo P, a na drugoj R1 i R2. Strana sa R1 i R2 ima kvorum i može da izabere R1 za novi primarni čvor. Strana sa čvorom P nema kvorum i ne može da izabere novi primarni čvor. Da su sva tri čvora u dve zone, na primer P i R1 u zoni 1, a R2 u zoni 2, odsecanje zone 1 ostavilo bi R2 bez kvoruma, pa bi otkaz jedne zone sprečio [[Failover|failover]].

## Napomene

Najčešći oblik je većinski kvorum: od n čvorova potrebno je više od polovine, odnosno ⌊n/2⌋ + 1. Svake dve većine imaju bar jedan zajednički čvor, pa u istom izboru ne mogu da postoje dve strane koje obe imaju kvorum. Zato se kod [[Izbor novog primarnog čvora|izbora novog primarnog čvora]] koristi neparan broj učesnika, najmanje tri.

Kvorum ne mora biti većina. Kod replikacije bez primarnog čvora koriste se posebni kvorumi za čitanje i za upis, čiji zbir mora biti veći od ukupnog broja čvorova, tako da svako čitanje vidi bar jedan čvor koji je primio poslednji potvrđeni upis.

Kvorum štiti od dve nezavisne odluke, ali ne zaustavlja čvor koji je odluku doneo ranije. Stari [[Primarni čvor|primarni čvor]] na strani bez kvoruma i dalje može da prihvata upise ako ga nešto drugo ne zaustavi, na primer [[Zakup uloge primarnog čvora|zakup uloge]] ili [[Fencing|fencing]].

Strana bez kvoruma ne može da napreduje ni kada su svi njeni čvorovi ispravni. Kvorum zato povećava bezbednost podataka po cenu dostupnosti na manjinskoj strani, što je primena [[Kompromis konzistentnosti i dostupnosti tokom mrežne particije|kompromisa konzistentnosti i dostupnosti]].
