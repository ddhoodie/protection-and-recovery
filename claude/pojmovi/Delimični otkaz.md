---
tip: pojam
aliases: [partial failure]
izvor: "George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, odeljak 1.5.5, https://www.pearson.com/en-us/subject-catalog/p/distributed-systems-concepts-and-design/P200000003160/9780132143011"
---
# Delimični otkaz (partial failure)

## Definicija

Delimični otkaz jeste stanje [[Distribuirani sistem|distribuiranog sistema]] u kojem je otkazala najmanje jedna, ali ne sve njegove komponente, tako da neke komponente i dalje funkcionišu, nezavisno od toga da li sistem kao celina i dalje pruža punu, umanjenu ili nikakvu zahtevanu funkcionalnost.

## Primer

U primarnom cloud kontekstu, primarni čvor replicirane baze doživi [[Otkaz komponente distribuiranog sistema|otkaz]], dok replike i [[Servisna instanca|servisne instance]] nastavljaju da rade. Poslovni tok koji zahteva upis u bazu ne može da napreduje, ali sistem nije prestao da se izvršava u celini. To je delimični otkaz čak i ako zbog značaja primarnog čvora korisniku privremeno nije dostupna glavna funkcija aplikativnog sistema.

## Napomene

Delimičnost se odnosi na to da je otkaz zahvatio samo deo komponenti, a ne nužno na stepen funkcionalnosti koji korisnik još dobija. Otkaz jedne kritične komponente može učiniti ceo [[Aplikativni sistem|aplikativni sistem]] nedostupnim iako njegove druge komponente i dalje rade. Obrnuto, redundansa može potpuno prikriti otkaz komponente, pa sistem spolja nastavlja da pruža punu funkcionalnost.

Granica posmatranog sistema utiče na klasifikaciju. Otkaz svih servisnih instanci jednog servisa može biti potpun otkaz tog servisa, ali istovremeno samo delimični otkaz šireg distribuiranog sistema čije druge komponente nastavljaju da rade. [[Zavisnost servisa|Zavisnosti servisa]] određuju koliko će se posledice početnog otkaza proširiti.
