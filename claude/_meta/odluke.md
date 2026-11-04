---
tip: odluke
---
# Odluke

## Pretpostavljeni pojmovi
Pojmovi koje publika zna bez definisanja. Ne otvaraju se ponovo osim na zahtev studenta.

- programiranje
- aplikacija
- baza podataka
- računarska mreža
- HTTP
- servisna komunikacija
- cloud infrastruktura
- softverska komponenta
- podatak
- poslovni cilj
- razmena poruka
- identitet izvršenja
- stanje izvršavanja
- funkcija
- balanser opterećenja
- procesor
- radna memorija
- virtualizacija
- izvršno okruženje
- proces
- dostupnost
- unutrašnje stanje sistema

## Promene konvencija

- 2026-10-31: „Razlikovanje pada procesa, usporenja i prekida mreže“ vodi se kao zaseban pojam, a ne kao veza između beležaka „Pad procesa“, „Usporavanje servisa“ i „Prekid mreže“, jer opisuje postupak procene na osnovu više opažanja, a ne razliku između definicija.
- 2026-10-21: Student trajno i unapred prihvata prvi predlog za svaki budući pojam. Posle provere izvora, tematskog obima, razgraničenja i slabosti, beleška se odmah upisuje bez dodatnog pitanja za potvrdu. Odluka zamenjuje istovetnu odluku od 2026-10-20 i važi dok je student izričito ne promeni.
- 2026-10-21: „Razlika između RTO i RPO“ vodi se kao uzajamno razgraničenje beležaka „Ciljno vreme oporavka“ i „Ciljna tačka oporavka“, a ne kao zaseban pojam.
- 2026-10-20: „Razlika između otkaza komponente i pada celog sistema“ vodi se kao veza između beležaka „Otkaz komponente distribuiranog sistema“ i „Potpuni otkaz sistema“, a ne kao zaseban pojam, da se definicije ne bi duplirale.

## Terminološke odluke

- 2026-10-20: Za stanje u kojem sistem ne pruža nijednu zahtevanu funkciju koristi se naziv „Potpuni otkaz sistema“. Izraz „potpuni pad sistema“ ostaje alias, jer „pad“ može neprecizno označavati i prestanak rada procesa ili pojedinačne komponente.
- 2026-10-31: Za `heartbeat` koristi se naziv „Signal života“, jer je glavni termin u bazi srpski. Izraz „heartbeat“ ostaje alias.
- 2026-10-31: Za `timeout` koristi se naziv „Rok čekanja“, jer je glavni termin u bazi srpski. Izraz „timeout“ ostaje alias.
- 2026-11-04: Proces je jedno izvršenje programa. Kad stane, novo pokretanje je drugi proces. Servisna instanca jeste taj proces jednog servisa. Čvor replicirane baze nije proces. Na njemu radi proces baze, i čvor može biti uključen dok je taj proces pao.

## Otvorena pitanja

- Razmotriti zasebne beleške za računski čvor, redundansu, zajednički uzrok otkaza, izolaciju otkaza, lančani otkaz, replikaciju, trajno stanje, sinhronu i asinhronu komunikaciju, mrežnu particiju, otkaz komunikacionog kanala, jačinu zavisnosti servisa, ciklus zavisnosti, redosled oporavka zavisnih komponenti, izvršenje i stanje poslovnog toka, konzistentno stanje toka, uzrok otkaza (`fault`), neispravno stanje (`error`), način otkaza (`failure mode`), zastoj procesa, latenciju zahteva, cilj nivoa usluge (SLO) i modele `crash-stop`, `crash-recovery` i `fail-stop`.


