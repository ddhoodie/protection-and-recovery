---
tip: pojam
aliases: [Recovery Point Objective, RPO]
izvor: "NIST Special Publication 800-34 Rev. 1, Contingency Planning Guide for Federal Information Systems, odeljak 3.2.1, https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-34r1.pdf"
---
# Ciljna tačka oporavka (Recovery Point Objective, RPO)

## Definicija

Ciljna tačka oporavka (RPO) jeste najranija prihvatljiva tačka u vremenu pre prekida do koje podaci [[Perzistentni sloj|perzistentnog sloja]] moraju moći da se oporave, čime se ograničava vremenski raspon promena podataka koje oporavak sme da izgubi.

## Primer

U primarnom cloud kontekstu, primarni čvor replicirane baze otkaže u 12:00, a za podatke [[Poslovni tok kroz više servisa i baza|poslovnog toka kroz više servisa i baza]] utvrđen je RPO od pet minuta. Oporavak mora da vrati stanje iz 11:55 ili novije. Ako najnovije ispravno obnovljeno stanje sadrži promene zaključno sa 11:58, RPO je ispunjen; ako sadrži samo promene zaključno sa 11:52, nije ispunjen.

## Napomene

Iako je RPO tačka u vremenu, u praksi se najčešće zadaje kao najduži prihvatljiv vremenski razmak između prekida i te tačke, na primer pet minuta. Taj razmak ograničava starost obnovljenog stanja, ali ne mora da odgovara broju izgubljenih zapisa jer učestalost promena podataka nije stalna.

RPO ne određuje koliko dugo oporavak sme da traje; tu granicu određuje [[Ciljno vreme oporavka]].
