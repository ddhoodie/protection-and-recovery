---
tip: pojam
aliases: [partition mode]
izvor: "Eric Brewer, CAP Twelve Years Later: How the \"Rules\" Have Changed, IEEE Computer, 45(2), 2012, str. 23-29"
---
# Režim rada tokom particije (partition mode)

## Definicija

Režim rada tokom particije jeste unapred određen način rada u koji komponenta [[Distribuirani sistem|distribuiranog sistema]] prelazi kada zaključi da ne može da komunicira sa delom sistema zbog moguće [[Mrežna particija|mrežne particije]], i u kojem ograničava operacije koje izvršava ili beleži dodatne podatke o izvršenim operacijama, kako bi posle particije podaci i [[Poslovni tok kroz više servisa i baza|poslovni tokovi]] mogli da se dovedu u konzistentno stanje.

## Primer

U primarnom cloud kontekstu, mrežna particija odvoji servis B, R1 i R2 od primarnog čvora P. Posle isteka [[Rok čekanja|roka čekanja]] prema čvoru P, servis B prelazi u režim rada tokom particije. Status poslovnog toka i dalje prikazuje sa replike, uz oznaku da može biti zastareo. Ne pokreće nove korake tokova, jer bi za to morao da upiše izmenu na primarni čvor. Svaki tok koji nije mogao da nastavi upisuje u lokalni spisak, sa vremenom i razlogom. Kada se veza vrati, taj spisak je ulaz za [[Oporavak posle mrežne particije|oporavak posle mrežne particije]].

## Napomene

[[Kompromis konzistentnosti i dostupnosti tokom mrežne particije|Kompromis konzistentnosti i dostupnosti]] je odluka o tome da li se pojedina vrsta zahteva odbija ili izvršava sa zastarelim podacima. Režim rada tokom particije je stanje komponente u kojem se te odluke primenjuju, zajedno sa beleženjem podataka potrebnih za kasniji oporavak.

Prelazak u režim donosi svaka komponenta za sebe, na osnovu sopstvenih opažanja. Ne postoji trenutak u kojem ceo sistem zna da je nastala particija, pa neke komponente mogu biti u režimu, a druge ne. Komponenta takođe ne mora moći da razlikuje particiju od otkaza drugog dela sistema, kao što opisuje [[Razlikovanje pada procesa, usporenja i prekida mreže|razlikovanje pada procesa, usporenja i prekida mreže]], pa isti režim važi za oba slučaja.

Režim rada tokom particije je jedan oblik degradiranog rada sistema. Degradirani rad je širi i može nastati i bez particije, na primer kada otkaže servis od kojeg se zavisi.
