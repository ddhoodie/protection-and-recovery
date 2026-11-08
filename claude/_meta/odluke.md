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
- čvor baze podataka
- potvrda izmene

## Promene konvencija

- 2026-10-31: „Razlikovanje pada procesa, usporenja i prekida mreže“ vodi se kao zaseban pojam, a ne kao veza između beležaka „Pad procesa“, „Usporavanje servisa“ i „Prekid mreže“, jer opisuje postupak procene na osnovu više opažanja, a ne razliku između definicija.
- 2026-10-21: Student trajno i unapred prihvata prvi predlog za svaki budući pojam. Posle provere izvora, tematskog obima, razgraničenja i slabosti, beleška se odmah upisuje bez dodatnog pitanja za potvrdu. Odluka zamenjuje istovetnu odluku od 2026-10-20 i važi dok je student izričito ne promeni.
- 2026-10-21: „Razlika između RTO i RPO“ vodi se kao uzajamno razgraničenje beležaka „Ciljno vreme oporavka“ i „Ciljna tačka oporavka“, a ne kao zaseban pojam.
- 2026-10-20: „Razlika između otkaza komponente i pada celog sistema“ vodi se kao veza između beležaka „Otkaz komponente distribuiranog sistema“ i „Potpuni otkaz sistema“, a ne kao zaseban pojam, da se definicije ne bi duplirale.
2026-11-08: Beleška konteksta navodi samo strukturu sistema (komponente, njihove veze i mehanizme). Pojedinačna ponašanja servisa koja služe jednom primeru, na primer zašto servis B čita status toka, ostaju u tom primeru i ne upisuju se u kontekst, pod uslovom da mu ne protivreče.

## Terminološke odluke

- 2026-10-20: Za stanje u kojem sistem ne pruža nijednu zahtevanu funkciju koristi se naziv „Potpuni otkaz sistema“. Izraz „potpuni pad sistema“ ostaje alias, jer „pad“ može neprecizno označavati i prestanak rada procesa ili pojedinačne komponente.
- 2026-10-31: Za `heartbeat` koristi se naziv „Signal života“, jer je glavni termin u bazi srpski. Izraz „heartbeat“ ostaje alias.
- 2026-10-31: Za `timeout` koristi se naziv „Rok čekanja“, jer je glavni termin u bazi srpski. Izraz „timeout“ ostaje alias.
- 2026-11-04: Proces je jedno izvršenje programa. Kad stane, novo pokretanje je drugi proces. Servisna instanca jeste taj proces jednog servisa. Čvor replicirane baze nije proces. Na njemu radi proces baze, i čvor može biti uključen dok je taj proces pao.
- 2026-11-06: „Čvor baze podataka“ vodi se kao pretpostavljen pojam, u značenju jednog samostalno pokrenutog primerka baze podataka koji čuva podatke i može imati ulogu primarnog čvora ili replike. U belešci „Računarski resurs“ reč „čvor“ označava računarski resurs (virtuelna mašina ili čvor koji pruža procesor i radnu memoriju), pa se u beleškama o replikaciji uvek koristi pun naziv „čvor baze podataka“.
- 2026-11-06: „Replika“ označava čvor baze podataka, a ne kopiju servisne instance, iako se isti izraz u nekim platformama koristi i za kopije servisa.
- 2026-11-08: „Konzistentnost podataka“ označava svojstvo replicirane baze koje određuje koliko podaci vraćeni čitanjem sa bilo kog čvora mogu da zaostaju za izmenama koje je primarni čvor potvrdio. Obuhvata nivoe od jake konzistentnosti (linearizabilnost) do konačne konzistentnosti. Za „strong consistency“ koristi se „jaka“, a ne „stroga“ konzistentnost. Ne označava zadovoljenost pravila nad podacima (značenje „C“ iz ACID), niti usklađenost stanja poslovnog toka, za koju se koristi izraz „konzistentno stanje toka“.
- 2026-11-08: „Dostupnost“ ostaje pretpostavljen pojam u opštem značenju. U belešci „CAP teorema“ i beleškama koje se na nju oslanjaju koristi se uže značenje iz teoreme: svaki čvor koji radi na svaki zahtev vraća odgovor koji nije greška. To uže značenje se navodi u samoj definiciji, a ne vodi se kao zaseban pojam.
- 2026-11-08: „Potvrda izmene“ vodi se kao pretpostavljen pojam, u značenju odgovora kojim primarni čvor javlja servisnoj instanci da je izmena podataka uspešno izvršena i trajno sačuvana (commit). Potvrđena izmena je izmena za koju je taj odgovor poslat. Prijem izmene na replici nije potvrda izmene u ovom smislu.

## Otvorena pitanja

- Razmotriti zasebne beleške za računski čvor, redundansu, zajednički uzrok otkaza, izolaciju otkaza, lančani otkaz, replikaciju, trajno stanje, sinhronu i asinhronu komunikaciju, otkaz komunikacionog kanala, jačinu zavisnosti servisa, ciklus zavisnosti, redosled oporavka zavisnih komponenti, izvršenje i stanje poslovnog toka, konzistentno stanje toka, uzrok otkaza (`fault`), neispravno stanje (`error`), način otkaza (`failure mode`), zastoj procesa, latenciju zahteva, cilj nivoa usluge (SLO) i modele `crash-stop`, `crash-recovery` i `fail-stop`.
