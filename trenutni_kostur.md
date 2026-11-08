I deo — Osnove distribuiranih sistema i otkaza

Celina 1 — Struktura distribuiranog sistema — Uroš Đošić

1. Distribuirani sistem
2. Aplikativni sistem
3. Servisna instanca
4. Perzistentni sloj
5. Računarski resurs
6. Zavisnost servisa
7. Graf zavisnosti
8. Poslovni tok kroz više servisa i baza
   Celina uvodi tri nivoa posmatranja: perzistentni sloj, aplikativne servise i poslovne tokove koji ih povezuju.
   Celina 2 — Priroda otkaza u distribuiranom sistemu — Stefan Nikolić
9. Otkaz komponente distribuiranog sistema
10. Delimični otkaz
11. Potpuni otkaz sistema
12. Jedinstvena tačka otkaza
13. Pad procesa
14. Usporavanje servisa
15. Prekid mreže
16. Širenje otkaza kroz graf zavisnosti
    Celina postavlja osnovni model otkaza i pokazuje zašto distribuirani sistem može nastaviti da radi iako su pojedini njegovi delovi neispravni.
    Celina 3 — Ciljevi i mere oporavka — Viktor Srbljin
17. Ciljno vreme oporavka
18. Ciljna tačka oporavka
19. Zajedničko merenje ostvarenja RTO i RPO
20. Vreme do ponovne dostupnosti servisa
21. Procenat uspešnih zahteva tokom otkaza
22. Broj tokova u nekonzistentnom stanju
23. Broj tokova u zaglavljenom stanju
24. Ukupno vreme oporavka sistema
    Ova celina razdvaja oporavak servisa, oporavak podataka i oporavak poslovnih tokova.
    II deo — Otkrivanje otkaza
    Celina 4 — Opservabilnost i detekcija otkaza — Nemanja Sovilj
25. Opservabilnost
26. Logovi
27. Metrike
28. Tragovi
29. Provera zdravlja servisne instance (health check)
30. Heartbeat
31. Timeout
32. Detekcija otkaza
33. Razlikovanje pada procesa, usporenja i prekida mreže
    Celina prati put od posmatranja sistema do odluke da je neka komponenta neispravna. Poseban naglasak je na činjenici da spor odgovor ne mora značiti pad komponente.
    III deo — Oporavak perzistentnog sloja
    Celina 5 — Replikacija i konzistentnost podataka - Ana Poparić
34. Primarni čvor
35. Replika
36. Primarni čvor i replike
37. Replicirana baza u cloud-u
38. Replikacija podataka sa primarnog čvora na replike
39. Konzistentnost podataka
40. Mrežna particija
41. CAP teorema
42. Kompromis konzistentnosti i dostupnosti tokom mrežne particije
    Celina uvodi model baze sa primarnim čvorom i replikama, a zatim ga povezuje sa mrežnom particijom i CAP teorijom.
    Celina 6 — Failover, split-brain i failback
43. Otkrivanje otkaza primarnog čvora
44. Razlikovanje pada primarnog čvora od njegovog usporenja
45. Pokretanje failover-a
46. Izbor novog primarnog čvora
47. Dva istovremena primarna čvora
48. Split-brain
49. Fencing
50. Neuspeli failover
51. Failback na prvobitni primarni čvor
    Redosled tema prati kompletan životni ciklus promene primarnog čvora: detekciju, izbor, zaštitu od paralelnog rada i eventualni povratak na prvobitni čvor.
    Celina 7 — Backup, PITR i gubitak podataka
52. Backup
53. Point-in-Time Recovery (PITR)
54. Replikacija, backup i PITR
55. Logička greška u podacima
56. Vraćanje baze na stanje pre logičke greške
57. Greška koja se replicira na sve čvorove
58. Slučajevi u kojima replikacija ne pomaže
59. Gubitak podataka u zavisnosti od mehanizma oporavka
60. Trajanje oporavka u zavisnosti od mehanizma oporavka
    Celina jasno razdvaja oporavak od pada čvora i oporavak od logički neispravne promene podataka.
    IV deo — Oporavak aplikativnih servisa
    Celina 8 — Orkestracija servisnih instanci
61. Aplikacija sa više servisnih instanci
62. Servisne instance iza balansera
63. Orkestracija servisnih instanci
64. Željeno stanje sistema
65. Uklanjanje neispravne instance iz saobraćaja
66. Restart servisne instance
67. Zamena servisne instance
68. Ponovno uključivanje instance u saobraćaj
69. Usmeravanje zahteva samo na ispravne instance
    Celina obrađuje oporavak računarskih resursa kao kontrolisani sled: otkrivanje, uklanjanje, restart ili zamena i vraćanje u saobraćaj.
    Celina 9 — Timeout, retry i circuit breaker
70. [Placeholder: pojam će biti određen]
71. Ponovno izvršavanje zahteva (retry)
72. Prolazni otkazi
73. Exponential backoff
74. Jitter
75. Retry bez backoff-a i jitter-a
76. Retry storm
77. Thundering herd
78. Circuit breaker i sprečavanje lančanog otkaza
    Celina počinje pojedinačnim zahtevom, a završava ponašanjem velikog broja klijenata koji istovremeno pokušavaju da pristupe servisu u oporavku.
    V deo — Konzistentnost poslovnih tokova
    Celina 10 — Saga i kompenzacione transakcije
79. Poslovni tok posle delimičnog otkaza
80. Distribuirana transakcija
81. Razlaganje distribuirane transakcije na lokalne korake
82. Saga
83. Kompenzaciona transakcija
84. Vraćanje toka u konzistentno stanje
85. Slučajevi u kojima kompenzacija nije moguća
86. Orkestracija Saga toka
87. Koreografija Saga toka
    Celina uvodi oporavak poslovne operacije koja je delimično izvršena u više servisa i baza.
    Celina 11 — Idempotentnost, outbox i trajno izvršavanje
88. Ponovno izvršavanje operacije
89. Dupli efekti ponovnog izvršavanja
90. Idempotentnost
91. Veza retry mehanizma i idempotentnosti
92. Transakcioni outbox
93. Objavljivanje događaja uz promenu u bazi
94. Trajno izvršavanje tokova (durable execution)
95. Kontrolne tačke (checkpointing)
96. Nastavak toka posle pada
    Celina povezuje pouzdano ponavljanje operacija, objavljivanje događaja i nastavak dugotrajnih tokova nakon otkaza.
    VI deo — Oporavak i provera celog sistema
    Celina 12 — Usklađivanje, redosled oporavka i testiranje
97. Tok u nekonzistentnom stanju
98. Zaglavljeni tok
99. Detekcija zaglavljenih tokova
100. Usklađivanje nekonzistentnih stanja (state reconciliation)
101. Redosled oporavka zavisnih komponenti
102. Određivanje redosleda oporavka prema grafu zavisnosti
103. Provera da je ceo sistem stvarno oporavljen
104. Ubrizgavanje otkaza (fault injection)
105. End-to-end testiranje otkaza i oporavka
     Završna celina povezuje sve prethodne slojeve. Oporavak se ne završava pokretanjem komponenti, već potvrdom da su zavisnosti, podaci i poslovni tokovi ponovo konzistentni.
     Konačni sled udžbenika
     Ukupna struktura prati klasičan didaktički napredak:
106. struktura distribuiranog sistema;
107. priroda delimičnih otkaza;
108. ciljevi i merenje oporavka;
109. posmatranje i detekcija problema;
110. replikacija i konzistentnost;
111. promena primarnog čvora;
112. oporavak podataka;
113. oporavak servisnih instanci;
114. otpornost servisnih poziva;
115. oporavak distribuiranih transakcija;
116. pouzdano izvršavanje tokova;
117. oporavak i testiranje sistema kao celine.
