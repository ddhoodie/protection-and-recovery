---
noteId: "4a291670d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "split brain"
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, poglavlje 5, https://dataintensive.net/"

---

# Split-brain

## Definicija

Split-brain jeste stanje u kojem više čvorova iste replicirane baze nezavisno prihvata upise kao [[Primarni čvor|primarni čvorovi]], bez međusobne koordinacije, pa se njihovi podaci razilaze.

## Primer

U primarnom cloud kontekstu, u 12:00 nastane [[Prekid mreže|prekid mreže]] koji primarni čvor P i servis A odvoji od replika R1 i R2 i servisa B. Nadzorna komponenta je na strani replika, ne dobija odgovore od čvora P i pokreće [[Failover|failover]], pa R1 postaje primarni čvor. Servis A i dalje upisuje na P, a servis B na R1. Isti zapis poslovnog toka na čvoru P dobije jednu izmenu, a na čvoru R1 drugu. Kada se veza ponovo uspostavi, nijedan čvor nema celo ispravno stanje, a sukobljene izmene ne mogu se automatski spojiti bez pravila za rešavanje sukoba.

## Napomene

U literaturi se izraz često koristi i za samo stanje u kojem dva čvora veruju da su primarna. Ova baza to stanje vodi kao [[Dva istovremena primarna čvora]], a split-brain označava tek razilaženje podataka usled nezavisnih upisa.

Razilaženje se ne otklanja samim gašenjem jednog čvora. Upisi jedne strane moraju da se odbace, spoje po unapred utvrđenom pravilu ili ručno usklade. Odbačeni upisi mogu biti već potvrđeni klijentima, pa predstavljaju gubitak podataka. Dok usklađivanje traje, [[Poslovni tok kroz više servisa i baza|poslovni tokovi]] koji su koristili oba čvora mogu ostati u nekonzistentnom stanju, što se meri kao [[Broj tokova u nekonzistentnom stanju|broj tokova u nekonzistentnom stanju]].

Čest uzrok je [[Mrežna particija|mrežna particija]]. Izbor većinom sprečava da strana bez većine izabere novi primarni čvor, ali stari primarni čvor na toj strani i dalje može da prihvata upise ako sam ne prestane. Zato je [[Fencing]] mera koja sprečava da drugi primarni čvor menja podatke.
