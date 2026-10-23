---
tip: pojam
aliases: [distributed system]
izvor: "George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, poglavlje 1, https://www.pearson.com/en-us/subject-catalog/p/distributed-systems-concepts-and-design/P200000003160/9780132143011"
---
# Distribuirani sistem (distributed system)

## Definicija

Distribuirani sistem jeste sistem čije hardverske ili softverske komponente izvršavaju rad na najmanje dva mrežno povezana računara, usklađuju svoje akcije razmenom poruka i zajedno ostvaruju funkcionalnost sistema, pri čemu komponente mogu da rade i otkazuju nezavisno jedna od druge.

## Primer

U primarnom cloud kontekstu, [[Servisna instanca|servisne instance]] i čvorovi replicirane baze rade na različitim mrežno povezanim računarima. Servisi razmenjuju zahteve, a čvorovi baze poruke replikacije kako bi zajedno izvršili poslovni tok. Ako jedna servisna instanca ili primarni čvor baze otkaže, ostale komponente mogu nastaviti da rade, iako poslovni tok možda neće moći da se završi dok se otkaz ne prevaziđe.

## Napomene

Sama mrežna povezanost ne čini skup računara distribuiranim sistemom. Komponente moraju koordinisano ostvarivati zajedničku funkcionalnost. Mogućnost nezavisnog otkaza ne garantuje izolaciju od zajedničkih uzroka otkaza.

