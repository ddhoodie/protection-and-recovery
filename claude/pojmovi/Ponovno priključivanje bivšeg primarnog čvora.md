---
tip: pojam
aliases: [rejoining a former primary, rollback]
izvor: "MongoDB Manual, Rollbacks During Replica Set Failover, https://www.mongodb.com/docs/manual/core/replica-set-rollbacks/"
---
# Ponovno priključivanje bivšeg primarnog čvora (rejoining a former primary)

## Definicija

Ponovno priključivanje bivšeg primarnog čvora jeste postupak kojim čvor baze podataka koji je izgubio ulogu [[Primarni čvor|primarnog čvora]] dok je bio odvojen od ostatka [[Replicirana baza u cloud-u|replicirane baze]] postaje [[Replika|replika]] novog primarnog čvora, tako što najpre odbacuje izmene koje je prihvatio, a koje nisu stigle do novog primarnog čvora, i zatim preuzima izmene novog primarnog čvora.

## Primer

U primarnom cloud kontekstu, [[Replikacija podataka sa primarnog čvora na replike|replikacija]] je asinhrona. [[Mrežna particija|Mrežna particija]] u 12:00:00 odvoji primarni čvor P od replika R1 i R2. Do isteka svog [[Zakup uloge primarnog čvora|zakupa]] u 12:00:08, P je servisu A potvrdio tri izmene koje nisu stigle do replika. R1 u 12:00:30 postaje primarni čvor i prihvata nove upise. U 12:06 veza se vraća. P utvrđuje da je R1 primarni čvor, pronalazi poslednju izmenu koju dele, odbacuje tri izmene koje R1 nema i čuva ih u zasebnom fajlu. Zatim preuzima izmene čvora R1 i od tada radi kao njegova replika.

## Napomene

Odbačene izmene su mogle biti potvrđene servisnim instancama, pa njihovo odbacivanje predstavlja gubitak podataka koji se poredi sa [[Ciljna tačka oporavka|RPO-om]]. Zato se odbačene izmene ne brišu bez traga, već se čuvaju da bi mogle da se pregledaju i ručno ponovo primene ako su još važeće.

Odbacivanje nije potrebno ako je primarni čvor potvrđivao izmene tek pošto ih primi većina čvorova. Takva izmena već postoji na čvoru koji je mogao da bude izabran za novi primarni čvor.

Ovaj postupak se razlikuje od [[Failback na prvobitni primarni čvor|failback-a]]. Ponovnim priključivanjem bivši primarni čvor postaje replika. Failback mu kasnije, kao posebna odluka, vraća ulogu primarnog čvora, a to je moguće tek kada je čvor ponovo priključen i ažuran.

Ako se bivši primarni čvor priključi bez odbacivanja, njegove izmene i izmene novog primarnog čvora mešaju se na istom zapisu, pa podaci čvorova ostaju razdvojeni kao kod [[Split-brain|split-brain-a]].
