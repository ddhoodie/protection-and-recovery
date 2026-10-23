---
tip: pojam
aliases: [successful request percentage during failure, request success rate during failure]
izvor: "Google, The Art of SLOs, odeljak Specifying an Availability SLI, https://sre.google/static/pdf/art-of-slos-handbook-a4.pdf"
---
# Procenat uspešnih zahteva tokom otkaza (successful request percentage during failure)

## Definicija

Procenat uspešnih zahteva tokom otkaza jeste odnos broja važećih zahteva koje je posmatrana funkcija uspešno obradila i ukupnog broja važećih zahteva koje je primila u unapred određenom intervalu otkaza, pomnožen sa 100.

## Primer

Tokom kontrolisanog [[Delimični otkaz|delimičnog otkaza]] jedne servisne instance, balanser u primarnom cloud kontekstu primi 10.000 važećih zahteva za posmatranu funkciju. Preostale [[Servisna instanca|servisne instance]] uspešno obrade 9.200 zahteva prema unapred utvrđenom kriterijumu, pa je procenat uspešnih zahteva tokom otkaza 92%.

## Napomene

Pre merenja moraju se odrediti granice intervala, šta zahtev čini važećim i šta znači uspešna obrada. HTTP odgovor ne mora biti uspešan samo zato što je primljen, a klijentski neispravan zahtev ne mora pripadati imeniocu.

Mera opisuje deo funkcije sačuvan tokom otkaza, dok [[Vreme do ponovne dostupnosti servisa]] opisuje koliko traje povratak zadatog nivoa funkcije. Procenat može prikriti razliku u poslovnom značaju zahteva i nestabilan je kada je broj zahteva mali, pa uz rezultat treba navesti broj zahteva i posmatrani interval.
