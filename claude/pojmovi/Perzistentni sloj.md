---
tip: pojam
aliases: [persistence layer]
izvor: "Microsoft, Using a Three-Tier Architecture Model, https://learn.microsoft.com/en-gb/windows/win32/cossdk/using-a-three-tier-architecture-model"
---
# Perzistentni sloj (persistence layer)

## Definicija

Perzistentni sloj jeste deo aplikacije odgovoran za upisivanje, trajno čuvanje i ponovno učitavanje podataka koji moraju ostati sačuvani nakon prestanka rada procesa ili [[Servisna instanca|servisne instance]]; obuhvata trajna skladišta podataka i mehanizme kojima im aplikacija pristupa.

## Primer

U primarnom cloud kontekstu, primarni čvor baze i njegove replike čine glavni deo perzistentnog sloja. Kada servisna instanca prestane da radi, podaci poslovnog toka ne smeju nestati zajedno sa njenim memorijskim stanjem, već se ponovo učitavaju iz baze. Kada primarni čvor baze doživi [[Otkaz komponente distribuiranog sistema|otkaz]], oporavak perzistentnog sloja zahteva da sačuvani podaci ponovo postanu dostupni i dovoljno ispravni za nastavak poslovnog toka.

## Napomene

Baza podataka je komponenta perzistentnog sloja, ali nije nužno ceo sloj. Memorijsko stanje servisne instance nije deo perzistentnog sloja ako se gubi njenim prestankom rada. Replikacija nije uslov perzistencije, već jedan od mehanizama dostupnosti i oporavka podataka.

