---
tip: pojam
aliases: [shard replication]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6, odeljak Partitioning and Replication, str. 200; Vitess Documentation, Shard, https://vitess.io/docs/concepts/shard/"
---
# Replikacija šarda (shard replication)

## Definicija

Replikacija šarda jeste održavanje kopija podataka jednog [[Šard|šarda]] na više čvorova baze podataka.

## Primer

U primarnom cloud kontekstu, izmene šarda S1 prenose se sa primarnog čvora P1 na R11 i R12, a izmene šarda S2 sa P2 na R21 i R22. Kada P1 otkaže, R11 može da preuzme njegovu ulogu, a šardovi S2 i S3 nastavljaju da primaju upise.

## Napomene

P1 i P2 nisu [[Dva istovremena primarna čvora|dva istovremena primarna čvora]], jer ne čuvaju iste podatke. Svaki je primarni samo za svoj šard.

Jedan čvor može biti primarni za jedan šard, a replika za drugi, pa njegov otkaz pogađa više šardova. Replikacija štiti od otkaza čvora samo ako kopije istog šarda nisu na istom [[Računarski resurs|računarskom resursu]].
