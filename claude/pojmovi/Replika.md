---
tip: pojam
aliases: [replica, standby, secondary]
izvor: "PostgreSQL 18 Documentation, Appendix M. Glossary, odrednica Replica (server), https://www.postgresql.org/docs/current/glossary.html"
---
# Replika (replica)

## Definicija

Replika jeste čvor baze podataka koji održava kopiju dela ili celokupnog skupa podataka [[Primarni čvor|primarnog čvora]].

## Primer

U primarnom cloud kontekstu, replike drže kopiju podataka poslovnog toka koje čuva primarni čvor. Kada primarni čvor otkaže, ispravna replika i dalje čuva svoju kopiju, pa podaci ostaju sačuvani na čvoru koji nije otkazao. Replika ipak ne mora da sadrži promene koje je primarni čvor primio neposredno pre otkaza, ako ih još nije primila.

## Napomene

Replika dobija izmene podataka koje potiču od primarnog čvora putem [[Replikacija podataka sa primarnog čvora na replike|replikacije]]. Te izmene mogu stizati sa zakašnjenjem, pa replika ne mora u svakom trenutku imati iste podatke kao primarni čvor i njeni podaci mogu biti stariji od njegovih.

Svrha replike je veća dostupnost podataka: kada primarni čvor otkaže, podaci i dalje postoje na replici, a replika može da preuzme njegovu ulogu. Neki sistemi repliku koriste i za čitanje podataka, pa baza može da posluži više zahteva.

Replika nije rezervna kopija (backup). Izmena koju primarni čvor primi prenosi se i na repliku, pa se u većini sistema pogrešna izmena pojavljuje i na replici.
