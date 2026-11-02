---
tip: kontekst
uloga: primarni
---
# Cloud sistem za oporavak

Cloud sistem služi kao zajednički kontekst za proučavanje delimičnih otkaza i oporavka podataka, servisa i poslovnih tokova.

## Elementi

- Više međuzavisnih [[Aplikativni servis|aplikativnih servisa]].
- Više servisnih instanci iza balansera opterećenja.
- Replicirana baza sa primarnim čvorom i replikama.
- Poslovni tok koji prolazi kroz više servisa i baza.
- Mehanizam za kontrolisano izazivanje otkaza.
- Logovi, metrike i tragovi koje tokom rada proizvode servisne instance i čvorovi baze i koji su dostupni van tih komponenti.
- Provere zdravlja kojima balanser opterećenja periodično ispituje servisne instance.
- Signali života koje primarni čvor replicirane baze periodično šalje replikama.
- Rokovi čekanja kojima servisi ograničavaju čekanje na odgovor zavisnih servisa.
