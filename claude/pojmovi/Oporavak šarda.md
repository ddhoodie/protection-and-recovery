---
tip: pojam
aliases: [shard recovery]
izvor: "MongoDB Manual, Backup and Restore Sharded Clusters, https://www.mongodb.com/docs/manual/administration/backup-sharded-clusters/; Microsoft, Azure Architecture Center, Sharding pattern, https://learn.microsoft.com/en-us/azure/architecture/patterns/sharding; Vitess Documentation, Reparenting, https://vitess.io/docs/user-guides/configuration-advanced/reparenting/"
---
# Oporavak šarda (shard recovery)

## Definicija

Oporavak šarda jeste postupak kojim se posle [[Otkaz šarda|otkaza šarda]] ponovo omogućavaju zahtevana čitanja i upisi njegovih podataka i obezbeđuje da [[Mapa šardova|mapa šardova]] upućuje zahteve na čvorove koji te podatke čuvaju.

## Primer

U primarnom cloud kontekstu, ako otkaže samo P2, dovoljan je [[Failover|failover]] na R21 i izmena mape. Ako sva tri čvora šarda S2 izgube podatke u 12:00, S2 se obnavlja iz rezervne kopije od 11:58, pa je [[Ciljna tačka oporavka|RPO]] od pet minuta ispunjen. Međutim, zapis da je tok 1.500.000 u 11:59 pokrenuo tok 2.500.000 izgubljen je sa S2, a zapisi pokrenutog toka postoje na S3.

## Napomene

Ispunjen RPO jednog šarda ne znači da su šardovi međusobno usklađeni. Moguće je vratiti sve šardove na isti trenutak, uz veći gubitak podataka, ili naknadno uskladiti pogođene tokove. Dok se to ne uradi, može ostati povećan [[Broj tokova u nekonzistentnom stanju|broj tokova u nekonzistentnom stanju]].

Kada su svi zapisi jednog toka u istom šardu, obnova šarda ih vraća na isti trenutak. Zato izbor [[Ključ šardovanja|ključa šardovanja]] utiče i na oporavak.
