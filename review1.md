### **Nedefinsani**, a pomenuti pojmovi:

1. aplikativni servis (ili ga dodati u odluke da ga svi vec razumiju ili ga definisati - sto je mozda bolje da ne bi doslo do nedoumica kada se pominje aplikativni sistem)
2. medjuzavisni tokovi - pomenut kao "raniji" pojam ali ipak nigdje definisan. Ukoliko nije dovoljno jasan onda ga je bolje nigdje ne korisiti (ni kao alijas) obzirom da dovodi do zabune
3. balanser - cesto se nalazi u primjerima, a nije definisan (mozda ga dodati u listu poznatih pojmova ako se ne uklapa u naredne prezentacije)
4. oporavak
5. dostupnost
6. otkaz (koristi se npr u definiciji _Procenat uspešnih zahteva tokom otkaza_) - ako nije redudantno obzirom da su odvojeno definisani djelimicni i potpuni otkaz
7. degradirani rezim - pominje se u napomeni za pojam _Širenje otkaza kroz graf zavisnosti_, a nije jasno sta se pod tim rezimom podrazumjeva

### **Nejasnosce/greske u definicijama:**

1.  U definiciji za _Procenat uspešnih zahteva tokom otkaza_ piše da se broje zahtevi primljeni tokom određenog intervala, ali nije objašnjeno kako se tretiraju zahtevi koji su primljeni tokom tog intervala, a završeni tek nakon njegovog isteka. Definicija i primer su u osnovi ispravni, ali nije dovoljno precizirano kako se tretiraju zahtevi koji su primljeni tokom posmatranog intervala, a završeni tek nakon njegovog isteka. Takođe, nije jasno kako se računaju zahtevi koji su na kraju intervala još u obradi ili su prekoračili dozvoljeno vreme obrade. Zbog toga različiti načini merenja mogu dovesti do različitih rezultata.

### **Nejasnoce/Greske u primjerima**:

1. Primjer za RPO - nije dovoljno da je obnovljeno stanje sadrži promene zaključno sa 11:58 nego je bitno naglasiti da **sadrži sve relevantne promene do te tačke i podaci su ispravni (konzistentni i neosteceni)**

2. Primjer za _Graf zavisnosti (dependency graph)_ kaze: Pri oporavku ovakav graf ukazuje da C treba osposobiti pre B, a B pre A.
   To zvuči kao da uvek moramo potpuno da oporavimo C pre nego što počnemo da oporavljamo B, a zatim potpuno oporavimo B pre nego što počnemo da oporavljamo A. Međutim, to nije uvek neophodno. Možemo da započnemo pripremu ili proveru servisa B dok se servis C još oporavlja. Bitno je da B ne može normalno da obavlja funkciju koja zavisi od C dok C nije spreman. Problem je u tome što beleška može da zvuči kao da servis B ne smemo ni da počnemo da oporavljamo dok C nije potpuno oporavljen. Ali to nije uvek tačno.
   Na primer, dok se baza C oporavlja, mi možemo da:
   - pokrenemo servis B;
   - proverimo da li se servis B pravilno pokreće;
   - pripremimo njegovu konfiguraciju.

   Međutim, B možda neće moći potpuno da radi dok C ne bude spreman.

   Dakle, možemo da počnemo sa oporavkom B, ali to ne znači da B već može normalno da funkcioniše.

### **Napomene**:

1. dodati reference u definisanju pojma _Zajedničko merenje ostvarenja RTO i RPO_ na RTO i RPO pojmove (pozeljno je stalno koristiti te skracenice (a ne mijesati kao u ovoj definiciji))
2. dodati pojam funkcija kao podrazumjevano poznat
