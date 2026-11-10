---
tip: pojam
aliases: [replication]
izvor: "PostgreSQL 18 Documentation, poglavlje 26, odeljak 26.2.5 Streaming Replication i odeljak 26.2.8 Synchronous Replication, https://www.postgresql.org/docs/18/warm-standby.html"
---
# Replikacija podataka sa primarnog čvora na replike (replication)

## Definicija

Replikacija podataka sa primarnog čvora na replike jeste prenošenje izmena podataka koje je izvršio [[Primarni čvor|primarni čvor]] do [[Replika|replika]], koje te izmene primenjuju na svojim kopijama podataka.

## Primer

U primarnom cloud kontekstu, servisna instanca servisa A upisuje podatke poslovnog toka u [[Replicirana baza u cloud-u|repliciranu bazu]]. Upis prima i izvršava primarni čvor, a zatim izmene šalje replikama. Svaka replika primenjuje primljenu izmenu na svojoj kopiji. Servisne instance ne upisuju direktno na replike.

## Napomene

Replikacija može biti sinhrona ili asinhrona. Kod sinhrone, primarni čvor potvrđuje izmenu tek kada je prime i replike od kojih se to zahteva, pa je upis sporiji, ali potvrđena izmena već postoji i na njima. Kod asinhrone, primarni čvor potvrđuje izmenu odmah, pa je upis brži, ali izmena koja još nije stigla do replika može biti izgubljena ako primarni čvor otkaže, što utiče na [[Ciljna tačka oporavka|ciljnu tačku oporavka]].
