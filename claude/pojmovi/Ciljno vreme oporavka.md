---
tip: pojam
aliases: [Recovery Time Objective, RTO]
izvor: "AWS Well-Architected Framework, Reliability Pillar, Disaster Recovery (DR) objectives, https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/disaster-recovery-dr-objectives.html"
---
# Ciljno vreme oporavka (Recovery Time Objective, RTO)

## Definicija

Ciljno vreme oporavka (RTO) jeste najduže prihvatljivo trajanje od prekida određene funkcije [[Aplikativni sistem|aplikativnog sistema]] do njenog ponovnog uspostavljanja u meri potrebnoj za ostvarivanje odgovarajućeg poslovnog cilja.

## Primer

U primarnom cloud kontekstu, primarni čvor replicirane baze otkaže u 12:00 i prekine [[Poslovni tok kroz više servisa i baza|poslovni tok kroz više servisa i baza]]. Za tu funkciju utvrđen je RTO od 10 minuta. Ako replika preuzme ulogu primarnog čvora, [[Servisna instanca|servisne instance]] ponovo uspostave veze i poslovni tok može da se nastavi u 12:08, cilj je ispunjen. Ako se to dogodi u 12:12, sistem se jeste oporavio, ali RTO nije ispunjen.

## Napomene

RTO je ciljna granica, a ne stvarno izmereno trajanje pojedinačnog oporavka. Njegova vrednost nije potpuna bez navedenog obima i kriterijuma ponovnog uspostavljanja funkcije. Pokrenut proces ili dostupna baza ne znače nužno da je poslovni tok ponovo upotrebljiv.

RTO ne određuje koliko promena podataka sme biti izgubljeno; tu granicu određuje [[Ciljna tačka oporavka]]. Takođe ne određuje procenat dostupnosti tokom dužeg perioda.
