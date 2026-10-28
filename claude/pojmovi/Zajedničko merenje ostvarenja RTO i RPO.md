---
tip: pojam
aliases: [joint RTO and RPO measurement, merenje RTO i RPO u istom scenariju otkaza]
izvor: "AWS Well-Architected Framework, Reliability Pillar, Disaster Recovery (DR) objectives, https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/disaster-recovery-dr-objectives.html"
---
# Zajedničko merenje ostvarenja RTO i RPO (joint RTO and RPO measurement)

## Definicija

Zajedničko merenje ostvarenja [[Ciljno vreme oporavka|RTO]] i [[Ciljna tačka oporavka|RPO]] jeste postupak u kojem se za isti kontrolisani prekid zasebno utvrđuju [[Vreme do ponovne dostupnosti servisa|trajanje do ponovnog uspostavljanja posmatrane funkcije]] i najnovija tačka u vremenu čije su promene podataka prisutne u obnovljenom stanju, a zatim se te ostvarene vrednosti porede sa [[Ciljno vreme oporavka|RTO]] i [[Ciljna tačka oporavka|RPO]].

## Primer

U primarnom cloud kontekstu, kontrolisani [[Delimični otkaz|delimični otkaz]] primarnog čvora baze nastane u 12:00. [[Poslovni tok kroz više servisa i baza|Poslovni tok kroz više servisa i baza]] ponovo može ispravno da se izvršava u 12:08, pa je ostvareno trajanje oporavka osam minuta. Najnovija promena prisutna u obnovljenoj bazi nastala je u 11:58, pa je ostvareni razmak gubitka podataka dva minuta. Te dve vrednosti porede se sa [[Ciljno vreme oporavka|RTO]] i [[Ciljna tačka oporavka|RPO]] utvrđenim za isti tok i isti način otkaza.

## Napomene

[[Ciljno vreme oporavka|RTO]] i [[Ciljna tačka oporavka|RPO]] su ciljne granice, a ne rezultati merenja. Isti početni trenutak i isti obim sistema omogućavaju da se brzina oporavka i starost obnovljenih podataka pripišu istoj strategiji i istom otkazu.

Rezultat nije pouzdan ako sistemi koji daju vremenske oznake nisu dovoljno usklađeni ili ako nije unapred određeno kada se funkcija smatra ponovo uspostavljenom. Uspešan odgovor provere zdravlja sam po sebi ne dokazuje da su zavisni servisi, podaci i poslovni tok spremni za upotrebu.
