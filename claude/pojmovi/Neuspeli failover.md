---
noteId: "4a57c790d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "failed failover"
  - "unsuccessful failover"
izvor: "Kleppmann, Designing Data-Intensive Applications, 5. poglavlje; PostgreSQL dokumentacija, odeljak o failover-u."
---

# Neuspeli failover (failed failover)

## Definicija

Neuspeli failover jeste [[Failover|failover]] posle kojeg baza ne prihvata upise preko tačno jednog ispravnog [[Primarni čvor|primarnog čvora]], zato što postupak nije završen ili je doveo do [[Split-brain|split-brain]] stanja.

## Primer

U primarnom cloud kontekstu, posle otkaza primarnog čvora P izabrana je replika R1, ali ona radi na manjoj virtuelnoj mašini i pod punim opterećenjem otkaže posle dva minuta. Replika R2 je u tom trenutku nedostupna, pa sistem ostaje bez primarnog čvora. U drugom slučaju R1 uspešno preuzme ulogu, ali adresa za upis nije preusmerena, pa [[Servisna instanca|servisne instance]] i dalje šalju upise na nedostupan čvor P. U trećem slučaju [[Fencing|fencing]] čvora P nije sproveden, pa P i R1 istovremeno prihvataju upise.

## Napomene

Promašen [[Ciljno vreme oporavka|RTO]] ili [[Ciljna tačka oporavka|RPO]] sam po sebi ne čini failover neuspelim. Sistem se u tom slučaju oporavio, ali cilj nije ispunjen, i to se meri posebno.

Nepotreban failover pokrenut zbog pogrešnog zaključka o otkazu ovde se računa kao uspešan ako je završen ispravno, iako može da nanese štetu.

Posle neuspelog failover-a sistem može biti u gorem stanju nego pre njega, jer je prvobitni primarni čvor i dalje otkazao, a deo replika možda više ne prima promene. Zato plan oporavka treba da predvidi i šta se radi kada failover ne uspe, na primer novi pokušaj sa drugom replikom ili vraćanje podataka iz rezervne kopije. Neuspeh se utvrđuje proverom da upisi zaista stižu na novi primarni čvor i da postoji tačno jedan čvor koji ih prihvata.
