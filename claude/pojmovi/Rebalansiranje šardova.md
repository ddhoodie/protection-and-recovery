---
tip: pojam
aliases: [rebalancing, shard rebalancing]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 6, odeljak Rebalancing Partitions, str. 209-214; Citus Documentation, Cluster Management, https://docs.citusdata.com/en/stable/admin_guide/cluster_management.html; MongoDB Manual, Sharded Cluster Balancer, https://www.mongodb.com/docs/manual/core/sharding-balancer-administration/"
---
# Rebalansiranje šardova (shard rebalancing)

## Definicija

Rebalansiranje šardova jeste premeštanje [[Šard|šardova]] ili njihovih delova sa jednih čvorova baze podataka na druge, kojim se menja podela podataka i zahteva među čvorovima.

## Primer

U primarnom cloud kontekstu, čvor P3 nema dovoljno prostora, pa se šard S3 premešta na veći čvor. Dok kopiranje traje, zahtevi idu na P3. Tek kada novi čvor primi i izmene nastale tokom kopiranja, [[Mapa šardova|mapa šardova]] se menja i zahtevi idu na njega. Ako se kopiranje prekine, P3 i dalje ima sve podatke.

## Napomene

Rebalansiranje nije [[Failover|failover]]: failover menja ulogu čvora koji već ima kopiju, a rebalansiranje premešta podatke.

Pre izmene [[Mapa šardova|mape šardova]] novi čvor mora da dobije i postojeće podatke i izmene nastale tokom kopiranja. Mapa se menja tek kada je potvrđeno da se podaci na novom čvoru poklapaju sa podacima na starom.

Ako se šard određuje ostatkom pri deljenju heša brojem šardova, prelazak sa tri na četiri šarda premešta oko 75% ključeva. Zato se često unapred pravi više šardova nego čvorova, pa se premeštaju celi šardovi.

Automatsko rebalansiranje je opasno uz automatsku [[Detekcija otkaza|detekciju otkaza]]: usporen čvor se proglasi neispravnim, a premeštanje njegovih podataka dodatno optereti i njega i ostale čvorove.
