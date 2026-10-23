I deo — Osnove distribuiranih sistema i otkaza

Celina 1 — Struktura distribuiranog sistema — Uroš Đošić
1. Distribuirani sistem
2. Aplikativni servis
3. Servisna instanca
4. Perzistentni sloj
5. Računarski resursi i aplikativni servisi
6. Zavisnosti servisa
7. Graf zavisnosti
8. Međuzavisni tokovi
9. Poslovni tok kroz više servisa i baza
Celina uvodi tri nivoa posmatranja: perzistentni sloj, aplikativne servise i poslovne tokove koji ih povezuju.
Celina 2 — Priroda otkaza u distribuiranom sistemu — Stefan Nikolić
1. Otkaz komponente distribuiranog sistema
2. Delimični otkaz
3. Potpuni pad sistema
4. Jedinstvena tačka otkaza (SPOF)
5. Pad procesa
6. Usporavanje servisa
7. Prekid mreže
8. Razlika između otkaza komponente i pada celog sistema
9. Širenje otkaza kroz graf zavisnosti
Celina postavlja osnovni model otkaza i pokazuje zašto distribuirani sistem može nastaviti da radi iako su pojedini njegovi delovi neispravni.
Celina 3 — Ciljevi i mere oporavka — Viktor Srbljin
1. Cilj vremena oporavka (RTO)
2. Cilj tačke oporavka (RPO)
3. Razlika između RTO i RPO
4. Merenje RTO i RPO u istom scenariju otkaza
5. Vreme do ponovne dostupnosti servisa
6. Procenat uspešnih zahteva tokom otkaza
7. Broj tokova u nekonzistentnom stanju
8. Broj tokova u zaglavljenom stanju
9. Ukupno vreme oporavka sistema
Ova celina razdvaja oporavak servisa, oporavak podataka i oporavak poslovnih tokova.
II deo — Otkrivanje otkaza
Celina 4 — Opservabilnost i detekcija otkaza
1. Opservabilnost
2. Logovi
3. Metrike
4. Tragovi
5. Provera zdravlja servisne instance (health check)
6. Heartbeat
7. Timeout
8. Detekcija otkaza
9. Razlikovanje pada procesa, usporenja i prekida mreže
Celina prati put od posmatranja sistema do odluke da je neka komponenta neispravna. Poseban naglasak je na činjenici da spor odgovor ne mora značiti pad komponente.
III deo — Oporavak perzistentnog sloja
Celina 5 — Replikacija i konzistentnost podataka
1. Primarni čvor
2. Replika
3. Primarni čvor i replike
4. Replicirana baza u cloud-u
5. Replikacija podataka sa primarnog čvora na replike
6. Konzistentnost podataka
7. Mrežna particija
8. CAP teorema
9. Kompromis konzistentnosti i dostupnosti tokom mrežne particije
Celina uvodi model baze sa primarnim čvorom i replikama, a zatim ga povezuje sa mrežnom particijom i CAP teorijom.
Celina 6 — Failover, split-brain i failback
1. Otkrivanje otkaza primarnog čvora
2. Razlikovanje pada primarnog čvora od njegovog usporenja
3. Pokretanje failover-a
4. Izbor novog primarnog čvora
5. Dva istovremena primarna čvora
6. Split-brain
7. Fencing
8. Neuspeli failover
9. Failback na prvobitni primarni čvor
Redosled tema prati kompletan životni ciklus promene primarnog čvora: detekciju, izbor, zaštitu od paralelnog rada i eventualni povratak na prvobitni čvor.
Celina 7 — Backup, PITR i gubitak podataka
1. Backup
2. Point-in-Time Recovery (PITR)
3. Replikacija, backup i PITR
4. Logička greška u podacima
5. Vraćanje baze na stanje pre logičke greške
6. Greška koja se replicira na sve čvorove
7. Slučajevi u kojima replikacija ne pomaže
8. Gubitak podataka u zavisnosti od mehanizma oporavka
9. Trajanje oporavka u zavisnosti od mehanizma oporavka
Celina jasno razdvaja oporavak od pada čvora i oporavak od logički neispravne promene podataka.
IV deo — Oporavak aplikativnih servisa
Celina 8 — Orkestracija servisnih instanci
1. Aplikacija sa više servisnih instanci
2. Servisne instance iza balansera
3. Orkestracija servisnih instanci
4. Željeno stanje sistema
5. Uklanjanje neispravne instance iz saobraćaja
6. Restart servisne instance
7. Zamena servisne instance
8. Ponovno uključivanje instance u saobraćaj
9. Usmeravanje zahteva samo na ispravne instance
Celina obrađuje oporavak računarskih resursa kao kontrolisani sled: otkrivanje, uklanjanje, restart ili zamena i vraćanje u saobraćaj.
Celina 9 — Timeout, retry i circuit breaker
1. Ograničavanje čekanja pomoću timeout-a
2. Ponovno izvršavanje zahteva (retry)
3. Prolazni otkazi
4. Exponential backoff
5. Jitter
6. Retry bez backoff-a i jitter-a
7. Retry storm
8. Thundering herd
9. Circuit breaker i sprečavanje lančanog otkaza
Celina počinje pojedinačnim zahtevom, a završava ponašanjem velikog broja klijenata koji istovremeno pokušavaju da pristupe servisu u oporavku.
V deo — Konzistentnost poslovnih tokova
Celina 10 — Saga i kompenzacione transakcije
1. Poslovni tok posle delimičnog otkaza
2. Distribuirana transakcija
3. Razlaganje distribuirane transakcije na lokalne korake
4. Saga
5. Kompenzaciona transakcija
6. Vraćanje toka u konzistentno stanje
7. Slučajevi u kojima kompenzacija nije moguća
8. Orkestracija Saga toka
9. Koreografija Saga toka
Celina uvodi oporavak poslovne operacije koja je delimično izvršena u više servisa i baza.
Celina 11 — Idempotentnost, outbox i trajno izvršavanje
1. Ponovno izvršavanje operacije
2. Dupli efekti ponovnog izvršavanja
3. Idempotentnost
4. Veza retry mehanizma i idempotentnosti
5. Transakcioni outbox
6. Objavljivanje događaja uz promenu u bazi
7. Trajno izvršavanje tokova (durable execution)
8. Kontrolne tačke (checkpointing)
9. Nastavak toka posle pada
Celina povezuje pouzdano ponavljanje operacija, objavljivanje događaja i nastavak dugotrajnih tokova nakon otkaza.
VI deo — Oporavak i provera celog sistema
Celina 12 — Usklađivanje, redosled oporavka i testiranje
1. Tok u nekonzistentnom stanju
2. Zaglavljeni tok
3. Detekcija zaglavljenih tokova
4. Usklađivanje nekonzistentnih stanja (state reconciliation)
5. Redosled oporavka zavisnih komponenti
6. Određivanje redosleda oporavka prema grafu zavisnosti
7. Provera da je ceo sistem stvarno oporavljen
8. Ubrizgavanje otkaza (fault injection)
9. End-to-end testiranje otkaza i oporavka
Završna celina povezuje sve prethodne slojeve. Oporavak se ne završava pokretanjem komponenti, već potvrdom da su zavisnosti, podaci i poslovni tokovi ponovo konzistentni.
Konačni sled udžbenika
Ukupna struktura prati klasičan didaktički napredak:
1. struktura distribuiranog sistema;
2. priroda delimičnih otkaza;
3. ciljevi i merenje oporavka;
4. posmatranje i detekcija problema;
5. replikacija i konzistentnost;
6. promena primarnog čvora;
7. oporavak podataka;
8. oporavak servisnih instanci;
9. otpornost servisnih poziva;
10. oporavak distribuiranih transakcija;
11. pouzdano izvršavanje tokova;
12. oporavak i testiranje sistema kao celine.