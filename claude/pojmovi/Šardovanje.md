---
tip: pojam
aliases: [sharding]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6 (Partitioning), str. 199-200; MongoDB Manual, Sharding, https://www.mongodb.com/docs/manual/sharding/; Vitess Documentation, Sharding, https://vitess.io/docs/reference/features/sharding/"
---
# Šardovanje (sharding)

## Definicija

Šardovanje jeste raspoređivanje istovrsnih podataka jedne baze podataka na više [[Šard|šardova]] smeštenih na više čvorova baze podataka.

## Primer

U primarnom cloud kontekstu, zapisi o koracima raspoređeni su na S1, S2 i S3, pa upise primaju primarni čvorovi P1, P2 i P3. Dodavanje replike ne bi rasteretilo upis, jer ona prima iste izmene.

## Napomene

Particionisanje tabele unutar jednog čvora relacione baze nije šardovanje, jer svi delovi ostaju na istom čvoru. Šardovanje nije ni [[Mrežna particija|mrežna particija]], koja je podela komunikacije, a ne podataka.

Šardovanje samo po sebi ne pravi kopije podataka, pa ne zamenjuje replikaciju.
