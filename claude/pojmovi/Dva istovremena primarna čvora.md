---
noteId: "4a0f73f0d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "dual primary"
  - "two simultaneous primaries"
izvor: "PostgreSQL Documentation, odeljak 26.3 Failover, https://www.postgresql.org/docs/current/warm-standby-failover.html"

---

# Dva istovremena primarna čvora (dual primary)

## Definicija

Dva istovremena primarna čvora jesu stanje u kojem dva čvora iste replicirane baze u istom trenutku imaju ulogu [[Primarni čvor|primarnog čvora]] ili se ponašaju kao da je imaju.

## Primer

U primarnom cloud kontekstu, primarni čvor P u 12:00 postane veoma spor zbog preopterećenja, pa nadzorna komponenta zaključi da je otkazao i replika R1 preuzme njegovu ulogu. Adresa za upis se preusmeri na R1. U 12:03 opterećenje čvora P opadne i on nastavi da radi, ne znajući za [[Failover|failover]], pa i dalje sebe smatra primarnim. Od tog trenutka postoje dva primarna čvora. Dok nijedna [[Servisna instanca|servisna instanca]] ne šalje upise na P, podaci se ne razilaze. Ako bi neka instanca sa zastarelom adresom ili ranije otvorenom vezom poslala upis na P, a P ga prihvatio, stanje bi prešlo u split-brain.

## Napomene

Ovo stanje je preduslov za [[Split-brain|split-brain]], ali nije isto što i on. Split-brain nastaje tek kada više čvorova nezavisno prihvata upise. Dva primarna čvora su opasna i kada još nema razilaženja podataka, jer je dovoljan jedan zalutao upis da do njega dođe.

Stanje najčešće nastaje kada se failover pokrene zbog pogrešnog zaključka da je primarni čvor pao, kada [[Mrežna particija|mrežna particija]] odvoji primarni čvor od ostalih, a druga strana izabere novi, ili kada se [[Failback na prvobitni primarni čvor|failback]] izvede pre nego što trenutni primarni čvor prestane da prihvata upise.

Stanje se prekida tako što jedan od čvorova izgubi ulogu. Stari primarni čvor može spolja da se zaustavi [[Fencing|fencing-om]], a pri ponovnom pokretanju može da proveri da li mu je uloga u međuvremenu oduzeta. Što stanje kraće traje, manja je verovatnoća da pređe u split-brain.
