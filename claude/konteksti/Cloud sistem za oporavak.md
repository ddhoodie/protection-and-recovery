---
tip: kontekst
uloga: primarni
---
# Cloud sistem za oporavak

Cloud sistem služi kao zajednički kontekst za proučavanje delimičnih otkaza i oporavka podataka, servisa i poslovnih tokova.

## Elementi

- Više međuzavisnih [[Aplikativni servis|aplikativnih servisa]].
- Više servisnih instanci iza balansera opterećenja.
- Replicirana baza sa primarnim čvorom P i replikama R1 i R2. Servisi upisuju samo na primarni čvor, a podatke mogu čitati i sa replika
- Nadzorna komponenta koja prati primarni čvor i može da pokrene failover.
- Poslovni tok koji prolazi kroz više servisa i baza.
- Mehanizam za kontrolisano izazivanje otkaza.
- Logovi, metrike i tragovi koje tokom rada proizvode servisne instance i čvorovi baze i koji su dostupni van tih komponenti.
- Provere zdravlja kojima balanser opterećenja periodično ispituje servisne instance.
- Signali života koje primarni čvor replicirane baze periodično šalje replikama.
- Rokovi čekanja kojima servisi ograničavaju čekanje na odgovor zavisnih servisa.
- Šardovana baza koraka, odvojena od replicirane baze sa čvorovima P, R1 i R2, u koju servisi upisuju zapis o svakom izvršenom koraku poslovnog toka. Podeljena je na šardove S1, S2 i S3. Svaki šard ima primarni čvor (P1, P2, P3) i dve replike (R11 i R12, R21 i R22, R31 i R32).
- Usmerivač zahteva, u više instanci, koji na osnovu svoje kopije mape šardova prosleđuje zahteve servisa čvorovima baze koraka. Mapa se čuva van šardova.
- Nadzorna komponenta prati i primarne čvorove šardova i može da pokrene failover pojedinačnog šarda.
- Rezervne kopije šardova, koje se prave zasebno za svaki šard.
