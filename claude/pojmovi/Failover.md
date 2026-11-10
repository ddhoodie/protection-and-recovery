---
noteId: "49bdaa70d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "database failover"
  - "primary failover"
izvor: "NIST SP 800-53 Rev. 5, preko NIST CSRC Glossary, https://csrc.nist.gov/glossary/term/failover; Microsoft, Failover and failback, https://learn.microsoft.com/en-us/azure/reliability/concept-failover-failback"
---

# Failover

## Definicija

Failover jeste postupak u kojem [[Replika|replika]] preuzima ulogu [[Primarni čvor|primarnog čvora]] posle stvarnog ili pretpostavljenog [[Otkaz komponente distribuiranog sistema|otkaza]] dotadašnjeg primarnog čvora, a zahtevi za upis se preusmeravaju na nju.

## Primer

U primarnom cloud kontekstu, primarni čvor P otkaže u 12:00. Nadzorna komponenta u 12:00:10 zaključi da je P otkazao i pokrene failover. Između replika R1 i R2 izabere R1, jer ima najnovije promene, i R1 počne da prihvata upise. Zatim se adresa za upis, preko koje se [[Servisna instanca|servisne instance]] povezuju sa bazom, preusmeri sa čvora P na R1. Instance do 12:08 ponovo uspostave veze i nastave [[Poslovni tok kroz više servisa i baza|poslovni tok]], pa je [[Ciljno vreme oporavka|RTO]] od 10 minuta ispunjen. Promene koje P pre otkaza nije stigao da replicira na R1 nisu prenete, i one čine gubitak podataka koji se poredi sa [[Ciljna tačka oporavka|RPO-om]].

## Napomene

Failover obuhvata [[Otkrivanje otkaza primarnog čvora|otkrivanje otkaza primarnog čvora]], [[Pokretanje failover-a|pokretanje failover-a]], [[Izbor novog primarnog čvora|izbor novog primarnog čvora]], preusmeravanje upisa i zaštitu od starog primarnog čvora pomoću [[Fencing|fencing-a]]. Failover je završen tek kada upisi stvarno stižu na novi primarni čvor, a ne već kada replika promeni ulogu.

Ako se promene sa primarnog čvora na replike prenose sa zakašnjenjem, poslednji upisi potvrđeni klijentima pre otkaza mogu nedostajati na replici koja preuzima ulogu. Failover zato može ispuniti RTO, a da gubitak podataka ipak bude veći od dozvoljenog po RPO-u.

Failover može biti automatski ili ručan. NIST pod failover-om podrazumeva automatsko prebacivanje, dok ova baza obuhvata oba načina. Planirana zamena uloga bez otkaza, na primer zbog održavanja, nije failover u ovom smislu. Izraz se u širem smislu koristi i za preusmeravanje saobraćaja na druge servisne instance, ali se u ovoj bazi odnosi na promenu primarnog čvora.
