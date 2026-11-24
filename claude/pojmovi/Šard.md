---
tip: pojam
aliases: [shard]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6 (Partitioning), str. 199; Microsoft, Azure Architecture Center, Sharding pattern, https://learn.microsoft.com/en-us/azure/architecture/patterns/sharding"
---
# Šard (shard)

## Definicija

Šard jeste jedan od delova na koje su podeljeni istovrsni podaci jedne baze podataka, tako da svaki podatak pripada tačno jednom delu i da svaki deo može biti smešten na čvorove baze podataka nezavisno od ostalih.

## Primer

U primarnom cloud kontekstu, baza koraka ima šardove S1, S2 i S3. Zapisi o koracima toka 42 pripadaju samo šardu S1. Njihove kopije na replikama tog šarda nisu novi šardovi.

## Napomene

U relacionoj bazi podatak je red tabele, a u dokument bazi dokument, pa šard sadrži deo redova ili dokumenata. Male tabele koje se cele kopiraju uz svaki šard nisu podeljene na šardove.

Šard nije [[Replika|replika]]: različiti šardovi sadrže različite podatke, a replika održava kopiju podataka.

Isti pojam u različitim sistemima ima različite nazive: „shard“ u MongoDB-u, Elasticsearch-u i Citus-u, „region“ u HBase-u, a „tablet“ u Bigtable-u. U literaturi je čest i naziv „partition“, ali se u ovoj bazi ne koristi za šard, da se ne bi mešao sa [[Mrežna particija|mrežnom particijom]]. U PostgreSQL-u „partition“ je deo tabele koji može ostati na istom čvoru.
