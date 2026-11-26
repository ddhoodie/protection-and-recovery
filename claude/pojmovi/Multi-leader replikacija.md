---
tip: pojam
aliases: [multi-leader replication, master-master replication, active/active replication]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Multi-leader replication; PostgreSQL Documentation, odeljak 27.1 Comparison of Different Solutions, odrednice Asynchronous Multimaster Replication i Synchronous Multimaster Replication, https://www.postgresql.org/docs/current/different-replication-solutions.html"
---
# Multi-leader replikacija (multi-leader replication)

## Definicija

Multi-leader replikacija jeste način replikacije u kome više [[Čvor replicirane baze|čvorova replicirane baze]] prima zahteve za upis, pri čemu svaki od njih upis izvršava lokalno i prosleđuje izmenu ostalim čvorovima.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu u kome sva četiri čvora primaju upise, servisna instanca servisa A u Regiji 1 upisuje status [[Poslovni tok kroz više servisa i baza|poslovnog toka]] na N1, a instanca servisa B u Regiji 2 upisuje status na N3. Svaki od ta dva čvora upis izvršava lokalno i prosleđuje izmenu ostalim čvorovima.

Otkaz čvora N1 ne zaustavlja upis u Regiji 1, jer i N2 prima upise. Kada Regija 1 otkaže u celini, instance u Regiji 2 i dalje upisuju na N3 i N4, bez [[Failover|failover-a]] i bez promene uloga čvorova. Kada se Regija 1 vrati, izmene primljene u Regiji 2 prenose se u nju. Izmene koje su čvorovi N1 i N2 primili, a nisu stigli da ih pošalju u Regiju 2, tamo nedostaju dok se Regija 1 ne vrati. Ako se ne vrati i ne postoji druga kopija tih izmena niti drugi način da se obnove, izgubljene su, a taj gubitak se poredi sa [[Ciljna tačka oporavka|ciljnom tačkom oporavka]].

## Napomene

Reč „leader“ ovde označava čvor koji prima upise i ne meša se sa [[Primarni čvor|primarnim čvorom]], koji je po definiciji jedini čvor ovlašćen za izmene. Zato se u beleškama o multi-leader i leaderless replikaciji koristi naziv „čvor replicirane baze“.

U primarnom kontekstu zahteve za upis prima samo primarni čvor P, koji je [[Jedinstvena tačka otkaza|jedinstvena tačka otkaza]] za upis dok ne postoji alternativa koja može da preuzme njegovu ulogu. Multi-leader replikacija uklanja tu zavisnost. Više čvorova koji primaju upise jeste predviđeno stanje ovog modela, za razliku od [[Dva istovremena primarna čvora|dva istovremena primarna čvora]], koja nastaju kao greška.

Prenos izmena između čvorova koji primaju upise najčešće je asinhron, pa se [[Sukob upisa|sukob upisa]] otkriva tek kada izmena stigne do drugog čvora. Sinhroni oblik postoji, ali tada svaki čvor pre potvrde upisa čeka ostale, čime se gubi glavna prednost modela. Dokumentacija PostgreSQL-a razlikuje asinhrono i sinhrono višestruko primanje upisa, a kod asinhronog navodi da se sukobi razrešavaju pravilima ili ih razrešavaju korisnici.

Prema knjizi, model se koristi za rad u više regija, za uređaje koji rade bez veze sa mrežom i za zajedničko uređivanje dokumenta. Unutar jedne regije korist retko opravdava dodatnu složenost.
