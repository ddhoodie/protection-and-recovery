---
tip: pojam
aliases: [partial network partition, partial partition]
izvor: "Mohammed Alfatafta, Basil Alkhatib, Ahmed Alquraan i Samer Al-Kiswany, Toward a Generic Fault Tolerance Technique for Partial Network Partitioning, 14th USENIX Symposium on Operating Systems Design and Implementation (OSDI 20), 2020, https://www.usenix.org/conference/osdi20/presentation/alfatafta"
---
# Delimična mrežna particija (partial network partition)

## Definicija

Delimična mrežna particija jeste [[Prekid mreže|prekid mreže]] pri kojem dve grupe komponenti [[Distribuirani sistem|distribuiranog sistema]] ne mogu međusobno da komuniciraju, dok bar jedna komponenta i dalje može da komunicira sa obe grupe.

## Primer

U primarnom cloud kontekstu, primarni čvor P je u zoni 1, replika R1 u zoni 2, a replika R2 u zoni 3. Veza između zone 1 i zone 2 prekida se u oba smera. R1 više ne prima [[Signal života|signale života]] od čvora P i za nju je P otkazao. R2 i dalje prima signale života od čvora P i poruke od R1, pa za nju P radi ispravno. Servisne instance u zonama 1 i 3 normalno upisuju na P. Ako se odluka o [[Failover|failover-u]] donese samo na osnovu opažanja čvora R1, sistem pokreće failover iako je P dostupan većini komponenti.

## Napomene

Delimična mrežna particija nije [[Mrežna particija|mrežna particija]] u smislu ove baze, jer komponente nisu podeljene u grupe koje su međusobno potpuno odsečene. Sistem je i dalje povezan, ali ne može svaka komponenta da komunicira sa svakom.

Opasnost je u tome što komponente imaju različitu sliku o istom stanju. Jedna komponenta zaključuje da je druga otkazala, a treća vidi obe kao ispravne. Mehanizmi koji pretpostavljaju da se sistem deli u odsečene grupe, na primer izbor većinom, mogu tada da ponavljaju promene primarnog čvora ili da pokrenu nepotreban failover.

Poseban slučaj je jednosmerna particija (simplex partition), kod koje poruke prolaze samo u jednom smeru. Na primer, R1 prima poruke od čvora P, ali odgovori čvora R1 ne stižu do njega.
