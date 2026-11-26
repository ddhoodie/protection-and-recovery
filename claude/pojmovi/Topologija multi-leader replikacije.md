---
tip: pojam
aliases: [replication topology, multi-leader replication topology]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Multi-leader replication topologies; MariaDB, Multi-Master Ring Replication, MariaDB dokumentacija, https://mariadb.com/docs/server/ha-and-performance/standard-replication/multi-master-ring-replication"
---
# Topologija multi-leader replikacije (multi-leader replication topology)

## Definicija

Topologija multi-leader replikacije jeste skup putanja kojima se izmena primljena na jednom čvoru prenosi do svih ostalih čvorova koji primaju upise u [[Multi-leader replikacija|multi-leader replikaciji]].

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu u kome sva četiri čvora primaju upise, u kružnoj topologiji (circular) N1 šalje izmene čvoru N2, N2 čvoru N3, N3 čvoru N4, a N4 čvoru N1, pri čemu svaki čvor uz izmene koje prosleđuje šalje i sopstvene. Kada N3 otkaže, N4 ne prima izmene čvora N2, iako je ispravan, sve dok se topologija ne rekonfiguriše tako da zaobiđe N3. U topologiji svaki sa svakim (all-to-all) N2 šalje izmene i direktno čvoru N4, pa otkaz N3 ne prekida tok između ostalih čvorova.

## Napomene

Knjiga navodi tri uobičajene topologije: kružnu, zvezdastu (star), u kojoj jedan korenski čvor prosleđuje izmene svim ostalim čvorovima, i topologiju svaki sa svakim. Zvezdasta se može uopštiti u stablo.

U kružnoj topologiji izmena prolazi kroz više čvorova, pa svaki čvor prosleđuje i izmene koje je primio od prethodnog. U zvezdastoj topologiji tu ulogu ima korenski čvor: on prosleđuje izmene svim ostalim čvorovima, dok ostali čvorovi ne moraju da ih prosleđuju jedni drugima. Da se izbegnu beskonačne petlje, izmena nosi identifikator čvora kroz koji je prošla, a čvor ignoriše izmenu koja nosi njegov identifikator. Dokumentacija MariaDB-a to opisuje za prsten: izmena koju je čvor napravio na kraju se vrati do njega, i on je prepoznaje i odbacuje.

Otkaz jednog čvora u kružnoj ili zvezdastoj topologiji prekida tok izmena između ostalih čvorova. Rekonfiguracija koja zaobilazi otkazali čvor u većini sistema se radi ručno, a pre nje otkaz mora da bude otkriven ([[Detekcija otkaza|detekcijom otkaza]]). Kod prekida veze između dva čvora u prstenu replikacija staje i, prema dokumentaciji MariaDB-a, sama se nastavlja kada se veza vrati, a čvorovi u međuvremenu opslužuju klijente lokalno.

Topologija svaki sa svakim otpornija je na otkaz jednog čvora, ali izmene mogu da prestignu jedna drugu: izmena može da stigne na čvor pre izmene od koje zavisi, na primer izmena reda pre upisa tog reda. To nije [[Sukob upisa|sukob upisa]], jer upisi nisu [[Istovremenost upisa|istovremeni]], ali se redosled ne može utvrditi satovima, koji nisu dovoljno pouzdani.

U primarnom kontekstu postoji samo jedna putanja izmena: [[Primarni čvor|primarni čvor]] P šalje izmene replikama R1 i R2 ([[Replikacija podataka sa primarnog čvora na replike|replikacija]]). Čvorovi ne šalju izmene jedni drugima, pa o izboru putanja nema šta da se odlučuje.
