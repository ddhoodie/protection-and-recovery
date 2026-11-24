---
tip: pojam
aliases: [shard failure, shard unavailability]
izvor: "MongoDB Manual, Sharding, odeljak High Availability, https://www.mongodb.com/docs/manual/sharding/; Microsoft, Azure Architecture Center, Sharding pattern, https://learn.microsoft.com/en-us/azure/architecture/patterns/sharding"
---
# Otkaz šarda (shard failure)

## Definicija

Otkaz šarda jeste stanje u kojem čvorovi baze podataka koji čuvaju kopije jednog [[Šard|šarda]] ne mogu da izvršavaju zahtevana čitanja ili upise njegovih podataka.

## Primer

U primarnom cloud kontekstu, P2 otkaže u 12:00:00, a R21 preuzme njegovu ulogu u 12:00:40. Za tih 40 sekundi S2 ne prima upise, a S1 i S3 ih primaju. Ako su upisi ravnomerni i ne ponavljaju se, [[Procenat uspešnih zahteva tokom otkaza|procenat uspešnih upisa]] iznosi oko 67%. Otkaz replike R22 ne bi bio otkaz šarda, jer P2 i dalje izvršava zahteve.

## Napomene

Za celu bazu ovo je [[Delimični otkaz|delimični otkaz]]. Zahtev kojem trebaju svi šardovi ipak ne može da bude potpuno izvršen. Ako je svaki od tri šarda nezavisno dostupan 99% vremena, sva tri su istovremeno dostupna oko 97% vremena.

Šardovanje zato može da smanji udeo podataka pogođen jednim otkazom, ali povećava broj delova koji mogu da otkažu.
