---
tip: pojam
aliases: [primary node, primary]
izvor: "PostgreSQL 18 Documentation, Chapter 26. High Availability, Load Balancing, and Replication, https://www.postgresql.org/docs/current/high-availability.html"
---
# Primarni čvor (primary node)

## Definicija

Među čvorovima baze podataka koji čuvaju kopije istih podataka, primarni čvor jeste jedini čvor koji je ovlašćen da prima i izvršava zahteve za izmenu tih podataka.

## Primer

U primarnom cloud kontekstu, servisne instance servisa A, B i C šalju [[Replicirana baza u cloud-u|repliciranoj bazi]] zahteve za upis podataka poslovnog toka, a te zahteve prima i izvršava samo primarni čvor. Kada primarni čvor otkaže, upis novih podataka nije moguć sve dok se ta funkcija ponovo ne uspostavi, pa poslovni tok koji zahteva upis privremeno ne može da napreduje. Ostali čvorovi baze su ispravni i sistem u celini nije prestao da radi, što je [[Delimični otkaz|delimični otkaz]].

## Napomene

Odrednica „primarni“ označava ovlašćenje za izmenu podataka, a ne jači računar ni važniji čvor. Izmene koje primarni čvor primi stižu do ostalih čvorova, pa su njegovi podaci izvor za njih.

Dok ne postoji operativno nezavisna alternativa koja može da preuzme njegovu ulogu, primarni čvor je [[Jedinstvena tačka otkaza|jedinstvena tačka otkaza]] za upis podataka, iako ostali čvorovi i dalje čuvaju podatke.

