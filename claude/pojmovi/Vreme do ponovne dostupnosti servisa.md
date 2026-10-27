---
tip: pojam
aliases: [time to service restoration, service recovery time]
izvor: "AWS Well-Architected Framework, Reliability Pillar, Disaster Recovery (DR) objectives, https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/disaster-recovery-dr-objectives.html"
---
# Vreme do ponovne dostupnosti servisa (time to service restoration)

## Definicija

Vreme do ponovne dostupnosti servisa jeste izmereno trajanje od trenutka kada funkcija koju pružaju njegove [[Servisna instanca|servisne instance]] prestane da zadovoljava unapred određeni, spolja proverljiv kriterijum uspeha do trenutka kada ga ponovo zadovolji.

## Primer

U primarnom cloud kontekstu, sve servisne instance jednog servisa postanu nedostupne u 14:00. Cloud platforma pokrene zamenske instance u 14:02, ali one tek u 14:03 mogu da obrade probne zahteve i pristupe zavisnoj bazi. Vreme do ponovne dostupnosti servisa iznosi tri minuta, jer samo pokretanje procesa u 14:02 još nije vratilo njegovu funkciju.

## Napomene

Kriterijum uspeha mora da odredi posmatranu funkciju, prihvatljiv odgovor i, kada je potrebno, period tokom kojeg rezultat mora ostati stabilan. Bez tog kriterijuma isto tehničko stanje može se različito proglasiti dostupnim.

Ova mera opisuje ostvareni rezultat konkretnog [[Delimični otkaz|otkaza]]. [[Ciljno vreme oporavka|Ciljno vreme oporavka]] je unapred određena najveća prihvatljiva vrednost sa kojom se rezultat poredi. Ako redundansa potpuno prikrije [[Delimični otkaz|otkaz]] jedne instance, vreme do ponovne dostupnosti funkcije servisa može biti nula iako zamena otkazale instance traje duže.
