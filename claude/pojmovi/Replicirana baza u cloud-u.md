---
tip: pojam
aliases: [replicated database in the cloud]
izvor: "Amazon RDS User Guide, Multi-AZ DB instance deployments for Amazon RDS, https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZSingleStandby.html"
---
# Replicirana baza u cloud-u (replicated database in the cloud)

## Definicija

Replicirana baza u cloud-u jeste baza podataka koju servisi koriste kao jednu bazu, a čine je [[Primarni čvor i replike|primarni čvor i replike]] raspoređeni na različitim [[Računarski resurs|računarskim resursima]] cloud infrastrukture.

## Primer

U primarnom cloud kontekstu, servisi A, B i C čuvaju podatke poslovnog toka u jednoj repliciranoj bazi. Primarni čvor i replike rade na različitim [[Računarski resurs|računarskim resursima]]. Kada računarski resurs primarnog čvora otkaže, replike na drugim računarskim resursima nastavljaju da rade, pa baza i dalje odgovara na čitanja, iako upis nije moguć.

## Napomene

Otkaz jednog čvora, dok ostali čvorovi rade, jeste [[Delimični otkaz|delimični otkaz]] baze. Da li je otkaz i [[Potpuni otkaz sistema|potpuni]] zavisi od toga koje funkcije baza još pruža, a to zavisi od toga koji je čvor otkazao.

Replike štite samo od otkaza koji ne pogađa sve čvorove istovremeno. Ako svi čvorovi zavise od istog računarskog resursa ili drugog zajedničkog uzroka otkaza, jedan događaj ih sve obara, kao što opisuje beleška [[Distribuirani sistem]]. Zato je za zaštitu važno da čvorovi budu smešteni na računarskim resursima koji ne dele zajednički uzrok otkaza.
