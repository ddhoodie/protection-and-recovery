---
tip: pojam
aliases: [concurrent writes, write concurrency, istovremeni upisi]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Detecting concurrent writes, podeljak The 'happens-before' relationship and concurrency; Leslie Lamport, Time, Clocks, and the Ordering of Events in a Distributed System, Communications of the ACM, 21(7), 1978, str. 558-565, https://amturing.acm.org/p558-lamport.pdf"
---
# Istovremenost upisa (concurrency of writes)

## Definicija

Istovremenost upisa jeste odnos dva upisa u kome nijedan od njih ne prethodi drugom, pri čemu jedan upis prethodi drugom kada onaj ko izvodi drugi upis ima saznanje o prvom, zavisi od njega ili ga nadovezuje.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu u kome sva četiri čvora primaju upise, [[Prekid mreže|prekid mreže]] između regija traje od 11:59 do 12:05. U 12:00:00 instanca servisa A u Regiji 1 upisuje na N1 status „plaćeno“, a u 12:00:01 instanca servisa B u Regiji 2 upisuje na N3 status „otkazano“. Nijedna instanca ni čvor ne zna za upis druge strane, pa su upisi istovremeni, iako je jedan izveden sekundu kasnije. Da je N3 primio status „plaćeno“ pre nego što je instanca servisa B upisala „otkazano“, drugi upis bi nadovezivao prvi i upisi ne bi bili istovremeni.

## Napomene

Istovremenost ne zavisi od sata. Dva upisa izvedena u razmaku od sekunde istovremena su ako nijedan izvođač nije znao za drugi, a upisi izvedeni gotovo u isti trenutak nisu istovremeni ako jedan nadovezuje drugi. Knjiga navodi da je zbog problema sa satovima u distribuiranim sistemima teško utvrditi da su dve stvari doslovno istovremene. Lamport odnos „happened before“ takođe definiše bez fizičkih satova i smatra dva događaja istovremenim kada nijedan ne prethodi drugom.

Istovremeni upisi nisu sami po sebi sukob. Ako menjaju različite podatke, ništa se ne sukobljava. [[Sukob upisa|Sukob upisa]] nastaje kada istovremeni upisi menjaju isti podatak. Za dva upisa istog podatka, ako jedan prethodi drugom, noviji zamenjuje raniji, a ako su istovremeni, sukob se mora [[Rešavanje sukoba|razrešiti]].

Isti odnos postoji u primarnom kontekstu, u primeru iz beleške [[Split-brain]]: servis A upisuje na čvor P, a servis B na čvor R1, i nijedan ne zna za upis drugog. Dok postoji samo jedan [[Primarni čvor|primarni čvor]], upisi istog podatka prolaze kroz njega i njihov redosled je poznat.

Brojevi verzija koje se pridružuju podatku omogućavaju da se bez satova utvrdi da li jedan upis prethodi drugom. Knjiga ih opisuje kao verzione vektore. Baza ih zasad ne definiše kao poseban pojam.
