---
tip: pojam
aliases: [total system recovery time, end-to-end system recovery time]
izvor: "NIST Special Publication 800-184, Guide for Cybersecurity Event Recovery, odeljak 3.4, https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-184.pdf"
---
# Ukupno vreme oporavka sistema (total system recovery time)

## Definicija

Ukupno vreme oporavka sistema jeste izmereno trajanje od nastanka posmatranog prekida do prvog trenutka kada [[Aplikativni sistem|aplikativni sistem]] ponovo zadovoljava sve unapred određene kriterijume oporavka za potrebne funkcije, podatke i pogođena izvršenja poslovnih tokova u utvrđenom obimu.

## Primer

U primarnom cloud kontekstu, kontrolisani otkaz primarnog čvora baze nastane u 12:00. [[Perzistentni sloj]] ponovo postane upotrebljiv u 12:06, servisne instance obrade probne zahteve u 12:08, a poslednja pogođena izvršenja [[Poslovni tok kroz više servisa i baza|poslovnog toka kroz više servisa i baza]] budu nastavljena ili bezbedno poništena u 12:14. Ako su time ispunjeni svi unapred određeni kriterijumi, ukupno vreme oporavka sistema iznosi 14 minuta, a ne osam minuta koliko je bilo potrebno samo za ponovno uspostavljanje servisne funkcije.

## Napomene

Obim sistema i kriterijumi završetka moraju biti utvrđeni pre merenja. Oni mogu obuhvatiti ponovnu dostupnost funkcija, prihvatljivo obnovljene podatke, obradu zaostalog rada i razrešenje pogođenih tokova. Bez toga se rezultat može proizvoljno skratiti proglašavanjem oporavka čim se komponente pokrenu.

Ukupno vreme nije nužno najveće pojedinačno [[Vreme do ponovne dostupnosti servisa|vreme do ponovne dostupnosti servisa]], jer provera zavisnosti i razrešavanje ranije pokrenutih tokova mogu trajati duže. Vrednosti [[Broj tokova u nekonzistentnom stanju|broja tokova u nekonzistentnom stanju]] i [[Broj tokova u zaglavljenom stanju|broja tokova u zaglavljenom stanju]] moraju dostići unapred prihvatljive granice ako su uključene u kriterijume završetka.
