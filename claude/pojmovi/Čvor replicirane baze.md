---
tip: pojam
aliases: [database node, replicated database node]
izvor: "PostgreSQL Documentation, High Availability, Warm Standby, https://www.postgresql.org/docs/current/warm-standby.html"
---
# Čvor replicirane baze (database node)

## Definicija

Čvor replicirane baze jeste jedan pokrenut primerak baze koji drži sopstvenu kopiju podataka i razmenjuje sa ostalim primercima iste baze poruke kojima se ta kopija održava usklađenom.

## Primer

U primarnom cloud kontekstu, jedan čvor prima upise [[Poslovni tok kroz više servisa i baza|poslovnog toka]]. Dva druga čvora primaju kopije tih upisa. Kad čvor koji prima upise doživi [[Otkaz komponente distribuiranog sistema|otkaz]], kopija podataka i dalje stoji na druga dva. [[Servisna instanca]] nije čvor baze: ona šalje upit, čvor ga upisuje.

## Napomene

Primarni čvor je onaj koji u datom trenutku prima upise. Replika je čvor koji drži kopiju. Oba su čvor replicirane baze.

Čvor replicirane baze nije teme u [[Graf zavisnosti|grafu zavisnosti]] i nije mašina koja samo daje procesor i radnu memoriju.
