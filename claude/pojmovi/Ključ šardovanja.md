---
tip: pojam
aliases: [shard key, sharding key]
izvor: "MongoDB Manual, Shard Keys, https://www.mongodb.com/docs/manual/core/sharding-shard-key/; Vitess Documentation, Vindexes, https://vitess.io/docs/reference/features/vindexes/; Citus Documentation, Choosing Distribution Column, https://docs.citusdata.com/en/stable/sharding/data_modeling.html; Citus Documentation, Creating and Modifying Distributed Objects (DDL), https://docs.citusdata.com/en/stable/develop/reference_ddl.html"
---
# Ključ šardovanja (shard key)

## Definicija

Ključ šardovanja jeste svojstvo podatka, ili skup svojstava, čija vrednost određuje kom [[Šard|šardu]] taj podatak pripada.

## Primer

U primarnom cloud kontekstu, ključ je ID [[Poslovni tok kroz više servisa i baza|poslovnog toka]], pa su svi zapisi o koracima jednog toka u istom šardu. Da je ključ ID koraka, zapisi istog toka mogli bi biti u više šardova, pa bi čitanje celog toka zavisilo od svih njih.

## Napomene

U relacionoj bazi ključ šardovanja čine jedna ili više kolona, a u dokument bazi jedno ili više polja. On ne mora biti primarni ključ: primarni ključ određuje red, a ključ šardovanja šard u kojem je red.

Upit koji ne sadrži vrednost ključa šardovanja mora da se pošalje svim šardovima, osim ako postoji indeks koji obuhvata podatke svih šardova. Zato otkaz jednog šarda može da spreči potpun odgovor.

Ako ograničenje jedinstvenosti ne obuhvata ključ šardovanja, jedan šard ne može sam da ga proveri, jer ista vrednost može postojati u drugom šardu.
