---
tip: pojam
aliases: [network partition, netsplit]
izvor: "George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, poglavlje 18 (Replication)"
---
# Mrežna particija (network partition)

## Definicija

Mrežna particija jeste [[Prekid mreže|prekid mreže]] koji deli komponente [[Distribuirani sistem|distribuiranog sistema]] u dve ili više grupa, tako da komponente unutar iste grupe mogu međusobno da komuniciraju, a komponente iz različitih grupa ne mogu.

## Primer

U primarnom cloud kontekstu, mrežna particija podeli sistem u dve grupe. Jednu čine [[Primarni čvor|primarni čvor]] i deo servisnih instanci, a drugu [[Replika|replike]] i ostale servisne instance. U prvoj grupi servisne instance i dalje upisuju na primarni čvor. U drugoj grupi replike više ne primaju izmene ni [[Signal života|signale života]] primarnog čvora, iako se on i dalje izvršava. Komponente u svakoj grupi rade ispravno, ali nijedna poruka ne prelazi iz jedne grupe u drugu.

## Napomene

Svaka mrežna particija jeste [[Prekid mreže|prekid mreže]], ali svaki prekid mreže nije particija. Ako otkaže jedan komunikacioni put, a komponente i dalje razmenjuju poruke drugim putem, sistem nije podeljen u grupe.

Particija je opasna zato što komponente u svakoj grupi nastavljaju da rade, a komponentama iz druge grupe izgledaju kao da su otkazale. Posledice po repliciranu bazu opisuju [[CAP teorema]] i [[Kompromis konzistentnosti i dostupnosti tokom mrežne particije|kompromis konzistentnosti i dostupnosti]].
