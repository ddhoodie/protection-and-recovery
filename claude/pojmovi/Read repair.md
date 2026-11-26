---
tip: pojam
aliases: [read repair]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Leaderless replication, podeljak Read repair and anti-entropy; Giuseppe DeCandia i drugi, Dynamo: Amazon's Highly Available Key-value Store, SOSP '07, 2007, odeljak 5 Implementation, https://www.cs.purdue.edu/homes/bb/cs590/papers/amazon-dynamo-sosp2007.pdf"
---
# Read repair

## Definicija

Read repair jeste popravka zastarele vrednosti na [[Čvor replicirane baze|čvoru replicirane baze]] koju izvodi klijent ili koordinator čitanja: kada se isti podatak čita sa više čvorova i odgovori se razlikuju, noviji odgovor se upisuje na čvor koji je vratio stariji.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu bez čvora koji određuje redosled upisa, N3 se posle otkaza vrati sa statusom poslovnog toka starijim od onog na N1 i N2 ([[Leaderless replikacija]]). Instanca servisa B čita status sa N2 i N3. N2 vraća noviji, a N3 stariji status. Instanca zatim upisuje noviji status na N3. Time se N3 za taj podatak oporavlja bez čekanja na [[Anti-entropy]].

## Napomene

Read repair radi dobro za podatke koji se često čitaju. Popravlja samo ono što je pročitano. Podatak koji se retko čita ostaje zastareo na čvoru koji ga nije primio, pa mu je trajnost smanjena. Ako čvor sa novim podatkom kasnije otkaže, vrednost može da se izgubi. Ovaj nedostatak popravlja [[Anti-entropy]]. Rad o Dynamo-u navodi da read repair popravlja replike koje su propustile skorašnju izmenu u zgodnom trenutku i rasterećuje Anti-entropy.

Read repair pretpostavlja da se zna koja je vrednost novija. Ako su vrednosti proizvod [[Istovremenost upisa|istovremenih upisa]], nijedna nije novija, pa to nije popravka nego [[Sukob upisa|sukob upisa]] koji se mora razrešiti.

U primarnom kontekstu replika R2 zaostaje za čvorom P, a izmene dobija od njega ([[Replikacija podataka sa primarnog čvora na replike|replikacija]]). Servis B koji čita sa R2 dobija stariji status, a čitanje R2 pri tom ništa ne popravlja: zastarela vrednost nestaje tek kada izmena stigne od P.

Naziv ostaje na engleskom, jer srpski prevod nije ustaljen.
