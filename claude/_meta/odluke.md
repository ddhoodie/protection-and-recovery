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
- metrika
- heš funkcija
- rezervna kopija
- zona dostupnosti

## Promene konvencija

- 2026-11-23: Celina 8 obrađuje mrežno particionisanje, a sharding ostaje celini 9. Beleške „Mrežna particija“, „CAP teorema“ i „Kompromis konzistentnosti i dostupnosti tokom mrežne particije“ iz celine 5 se ne ponavljaju, već se linkuju. Celina 8 pokriva zaštitu tokom particije i oporavak posle nje.
- 2026-11-23: „Izlečenje mrežne particije“ ne vodi se kao zaseban pojam, već je spojen sa beleškom „Oporavak posle mrežne particije“ kao njen početni trenutak. Izraz ostaje alias.
- 2026-11-23: „Kvorum“ definiše celina 8, dovoljno opšte da obuhvati i većinski kvorum za izbor primarnog čvora i kvorume čitanja i upisa kod replikacije bez primarnog čvora iz celine 7. Celina 7 ga linkuje i ne pravi zasebnu belešku.
- 2026-11-07: „Razlikovanje pada primarnog čvora od njegovog usporenja“ spojeno je sa beleškom „Otkrivanje otkaza primarnog čvora“, jer je uži slučaj pojma „Razlikovanje pada procesa, usporenja i prekida mreže“ iz celine 4. U beleški ostaje samo ono što je specifično za primarni čvor. Na oslobođeno mesto u kosturu celine 6 dolazi „Failover“ kao prvi pojam.

- 2026-10-31: „Razlikovanje pada procesa, usporenja i prekida mreže“ vodi se kao zaseban pojam, a ne kao veza između beležaka „Pad procesa“, „Usporavanje servisa“ i „Prekid mreže“, jer opisuje postupak procene na osnovu više opažanja, a ne razliku između definicija.
- 2026-10-31: Beleške celine 6 upisane su posle dogovora sa studentom, pa konvencija o unapred prihvaćenom prvom predlogu od 2026-10-21 za njih nije primenjena.
- 2026-10-31: U celinu 6 dodata je beleška „Failover“, koje nema u kosturu, jer je koriste „Pokretanje failover-a“ i „Neuspeli failover“.
- 2026-10-31: Promašen RTO ili RPO sam po sebi ne čini failover neuspelim, već se meri posebno.
- 2026-10-21: Student trajno i unapred prihvata prvi predlog za svaki budući pojam. Posle provere izvora, tematskog obima, razgraničenja i slabosti, beleška se odmah upisuje bez dodatnog pitanja za potvrdu. Odluka zamenjuje istovetnu odluku od 2026-10-20 i važi dok je student izričito ne promeni.
- 2026-10-21: „Razlika između RTO i RPO“ vodi se kao uzajamno razgraničenje beležaka „Ciljno vreme oporavka“ i „Ciljna tačka oporavka“, a ne kao zaseban pojam.
- 2026-10-20: „Razlika između otkaza komponente i pada celog sistema“ vodi se kao veza između beležaka „Otkaz komponente distribuiranog sistema“ i „Potpuni otkaz sistema“, a ne kao zaseban pojam, da se definicije ne bi duplirale.
- 2026-11-08: Beleška konteksta navodi samo strukturu sistema (komponente, njihove veze i mehanizme). Pojedinačna ponašanja servisa koja služe jednom primeru, na primer zašto servis B čita status toka, ostaju u tom primeru i ne upisuju se u kontekst, pod uslovom da mu ne protivreče.
- 2026-11-26: Korišćenje sekundarnog konteksta [[Cloud sistem u dve regije]] za pojmove Celine 7 odobreno je na PR review-u. Primeri iz primarnog konteksta su izuzetak kada on ne može da predstavi pojam, što je slučaj kod multi-leader i leaderless replikacije, jer primarni kontekst opisuje samo model u kome upise prima jedan čvor. U tim beleškama odeljak „Primer“ stoji u sekundarnom kontekstu i to izričito navodi, a primarni kontekst se pominje u napomenama radi poređenja. Kontekst je naveden u odeljku „Sekundarni konteksti“ u `_meta/konfiguracija.md`.

## Terminološke odluke

- 2026-11-23: „Delimična mrežna particija“ nije podvrsta pojma „Mrežna particija“ u smislu ove baze, jer komponente nisu podeljene u međusobno potpuno odsečene grupe. Naziv se zadržava jer je ustaljen u literaturi (partial network partition), a razgraničenje je u napomenama obe beleške.
- 2026-11-23: Za `leader lease` koristi se naziv „Zakup uloge primarnog čvora“, jer je glavni termin u bazi srpski. Izraz „lease“ ostaje alias.
- 2026-11-23: „Režim rada tokom particije“ je uži pojam od degradiranog rada sistema. Degradirani rad (pominje se u beleški „Širenje otkaza kroz graf zavisnosti“) i dalje nema belešku.
- 2026-11-09: RTO je ciljna granica, a ne vreme koje se „troši“ ili u koje nešto „ulazi“. Vreme detekcije, izbora ili fencing-a ulazi u ostvareno trajanje oporavka, a to trajanje se poredi sa RTO-om. Primenjeno u beleškama celine 6 po uzoru na belešku „Detekcija otkaza“.

- 2026-10-31: „Dva istovremena primarna čvora“ označava stanje uloga, a „Split-brain“ stanje u kojem više čvorova nezavisno prihvata upise, pa se podaci razilaze. U literaturi se ovi izrazi često koriste kao sinonimi.
- 2026-10-31: Termini „Failover“, „Failback“, „Fencing“ i „Split-brain“ ostaju na engleskom, jer srpski prevodi nisu ustaljeni.
- 2026-10-20: Za stanje u kojem sistem ne pruža nijednu zahtevanu funkciju koristi se naziv „Potpuni otkaz sistema“. Izraz „potpuni pad sistema“ ostaje alias, jer „pad“ može neprecizno označavati i prestanak rada procesa ili pojedinačne komponente.
- 2026-10-31: Za `heartbeat` koristi se naziv „Signal života“, jer je glavni termin u bazi srpski. Izraz „heartbeat“ ostaje alias.
- 2026-10-31: Za `timeout` koristi se naziv „Rok čekanja“, jer je glavni termin u bazi srpski. Izraz „timeout“ ostaje alias.
- 2026-11-04: Proces je jedno izvršenje programa. Kad stane, novo pokretanje je drugi proces. Servisna instanca jeste taj proces jednog servisa. Čvor replicirane baze nije proces. Na njemu radi proces baze, i čvor može biti uključen dok je taj proces pao.
- 2026-11-06: „Čvor baze podataka“ vodi se kao pretpostavljen pojam, u značenju jednog samostalno pokrenutog primerka baze podataka koji čuva podatke i može imati ulogu primarnog čvora ili replike. U belešci „Računarski resurs“ reč „čvor“ označava računarski resurs (virtuelna mašina ili čvor koji pruža procesor i radnu memoriju), pa se u beleškama o replikaciji uvek koristi pun naziv „čvor baze podataka“.
- 2026-11-06: „Replika“ označava čvor baze podataka, a ne kopiju servisne instance, iako se isti izraz u nekim platformama koristi i za kopije servisa.
- 2026-11-08: „Konzistentnost podataka“ označava svojstvo replicirane baze koje određuje koliko podaci vraćeni čitanjem sa bilo kog čvora mogu da zaostaju za izmenama koje je primarni čvor potvrdio. Obuhvata nivoe od jake konzistentnosti (linearizabilnost) do konačne konzistentnosti. Za „strong consistency“ koristi se „jaka“, a ne „stroga“ konzistentnost. Ne označava zadovoljenost pravila nad podacima (značenje „C“ iz ACID), niti usklađenost stanja poslovnog toka, za koju se koristi izraz „konzistentno stanje toka“.
- 2026-11-08: „Dostupnost“ ostaje pretpostavljen pojam u opštem značenju. U belešci „CAP teorema“ i beleškama koje se na nju oslanjaju koristi se uže značenje iz teoreme: svaki čvor koji radi na svaki zahtev pre ili kasnije vrati odgovor koji nije greška. To uže značenje se navodi u samoj definiciji, a ne vodi se kao zaseban pojam.
- 2026-11-08: „Potvrda izmene“ vodi se kao pretpostavljen pojam, u značenju odgovora kojim primarni čvor javlja servisnoj instanci da je izmena podataka uspešno izvršena i trajno sačuvana (commit). Potvrđena izmena je izmena za koju je taj odgovor poslat. Prijem izmene na replici nije potvrda izmene u ovom smislu.
- 2026-11-13: Beleška „Metrika“ preimenovana je u „Metrika trajanja odgovora“, jer je opšti pojam metrike preširok za celinu 4, a mere oporavka iz celine 3 takođe mogu da se nazovu metrikama. Uži pojam odgovara primeru i naglasku celine da spor odgovor ne mora značiti pad komponente. „Metrika“ u opštem značenju vodi se kao pretpostavljen pojam.
- 2026-11-23: „Particija“ označava podelu mreže, a „šard“ deo podataka, iako se u literaturi za šard koristi i izraz „partition“. Izuzetak je „particionisanje tabele“, ustaljen naziv za podelu tabele unutar jednog čvora. Za `sharding` koristi se „Šardovanje“, a engleski izraz ostaje alias.
- 2026-11-23: U beleškama o šardovanju koristi se „čvor baze podataka“, jer šard ne mora biti repliciran.
- Predlog Celine 7, nije usvojeno: U beleškama o multi-leader i leaderless replikaciji za čvorove koji primaju upise koristi se „čvor replicirane baze“, a ne „primarni čvor“ ni „replika“, jer se te dve beleške odnose na model sa jednim čvorom koji prima upise.
- Predlog Celine 7, nije usvojeno: „Multi-leader replikacija“, „Leaderless replikacija“, „Sloppy kvorum“, „Read repair“ i „Anti-entropy“ zadržavaju engleski izraz u nazivu, jer srpski prevodi nisu ustaljeni, kao kod termina „Failover“ i „Split-brain“.
- Predlog Celine 7, nije usvojeno: „Kvorum“ je jedna beleška sa dva oblika istog pojma: većinski kvorum (primarni kontekst, izbor novog primarnog čvora) i kvorum za čitanje i upis (w, r, sekundarni kontekst, leaderless replikacija). Oblici se razlikuju u odeljcima „Primer“ i „Napomene“, a beleške Celine 7 linkuju na odeljak „O kvorumu za čitanje i upis“.
- Predlog Celine 7, nije usvojeno: „Istovremenost upisa“ određuje se preko saznanja jednog upisa o drugom, a ne preko vremena. „Sukob upisa“ označava istovremene upise istog podatka na različitim čvorovima. Za razliku od njega, „Split-brain“ označava stanje u kome su čvorovi nezavisno prihvatali upise kao primarni.

## Otvorena pitanja

- Razmotriti zasebne beleške za računski čvor, redundansu, zajednički uzrok otkaza, izolaciju otkaza, lančani otkaz, replikaciju, trajno stanje, sinhronu i asinhronu komunikaciju, otkaz komunikacionog kanala, jačinu zavisnosti servisa, ciklus zavisnosti, redosled oporavka zavisnih komponenti, izvršenje i stanje poslovnog toka, konzistentno stanje toka, uzrok otkaza (`fault`), neispravno stanje (`error`), način otkaza (`failure mode`), zastoj procesa, latenciju zahteva, cilj nivoa usluge (SLO) i modele `crash-stop`, `crash-recovery` i `fail-stop`.
- Proveriti u originalu navode iz beleški „Split-brain“ (Kleppmann, DDIA, poglavlje 5) i „Izbor novog primarnog čvora“ (Raft). Ti tekstovi nisu pročitani, već samo sekundarni izvori.
