---
tip: pojam
aliases: [data distribution across shards, range sharding, hash sharding]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6, odeljci Partitioning by Key Range i Partitioning by Hash of Key, str. 202-204; MongoDB Manual, Sharding, odeljci Hashed Sharding i Ranged Sharding, https://www.mongodb.com/docs/manual/sharding/"
---
# Raspodela podataka po šardovima (data distribution across shards)

## Definicija

Raspodela podataka po šardovima jeste pravilo koje vrednosti [[Ključ šardovanja|ključa šardovanja]] pridružuje [[Šard|šard]]. Kod raspodele po opsegu svaki šard obuhvata neprekidan raspon vrednosti ključa, a kod raspodele po hešu šard se određuje iz vrednosti heš funkcije nad ključem.

## Primer

U primarnom cloud kontekstu, po opsegu S1 sadrži tokove do 1.000.000, S2 od 1.000.001 do 2.000.000, a S3 ostale. Novi tokovi dobijaju rastuće ID-jeve iznad 2.000.000, pa svi idu na S3. Dok je S3 nedostupan, upis njihovih koraka nije moguć. Uz ravnomernu raspodelu po hešu, isti otkaz pogađa oko trećine novih tokova, ali čitanje tokova od 1.000 do 2.000 može da zahteva sva tri šarda.

## Napomene

Opseg olakšava čitanje uzastopnih vrednosti ključa, a heš ravnomernije raspoređuje ključeve. Heš ne pomaže kada većina zahteva cilja istu vrednost ključa.
