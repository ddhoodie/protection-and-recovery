---
tip: pojam
aliases: [failure detection, otkrivanje otkaza]
izvor: "Tushar Deepak Chandra i Sam Toueg, Unreliable Failure Detectors for Reliable Distributed Systems, Journal of the ACM, 43(2), 1996, uvod, https://cs.nyu.edu/~apanda/classes/sp25/papers/chandra-toueg.pdf"
---
# Detekcija otkaza (failure detection)

## Definicija

Detekcija otkaza jeste postupak kojim se, na osnovu dostupnih opažanja, donosi odluka da se smatra da je komponenta [[Distribuirani sistem|distribuiranog sistema]] doživela [[Otkaz komponente distribuiranog sistema|otkaz]], pri čemu ta odluka može da bude pogrešna.

## Primer

U primarnom cloud kontekstu, balanser opterećenja izvodi [[Provera zdravlja servisne instance|proveru zdravlja]] nad svakom [[Servisna instanca|servisnom instancom]] servisa B svakih 10 s, uz [[Rok čekanja|rok čekanja]] od 2 s. Kada jedna instanca dva puta uzastopno ne odgovori, balanser je proglašava otkazalom. To proglašavanje je detekcija otkaza, a prestanak slanja zahteva toj instanci je reakcija na nju.

Odluka je ispravna ako je nastao [[Pad procesa|pad procesa]] te instance. Ispravna je i ako je proces živ, a odgovor na proveru koja koristi sporu bazu stiže ispravan, ali posle 3 s: vreme je preko granice, pa otkaz postoji, kao što opisuje beleška [[Usporavanje servisa]]. Tada ne stoji zaključak da je proces pao, a ponovno pokretanje te instance ne ubrzava bazu. Odluka je pogrešna ako je [[Prekid mreže|prekid mreže]] između balansera i instance sprečio provere, a instanca i dalje radi ispravno. Moguća je i suprotna greška: instanca koja prolazi proveru, a ne može da obavi svoju funkciju, ostaje neotkrivena.

## Napomene

[[Otkaz komponente distribuiranog sistema|Otkaz]] je događaj na komponenti, a detekcija je odluka o tom događaju. Otkaz može da ostane neotkriven, a detekcija može da proglasi otkaz koji nije nastao.

Detekcija se ocenjuje prema tome da li otkazi budu otkriveni, koliko često se ispravne komponente pogrešno proglase otkazalim i koliko brzo se odluka donese. Te zahteve je teško ispuniti istovremeno, jer duže čekanje smanjuje broj pogrešnih odluka, ali odlaže otkrivanje. Zato je pitanje koja je greška skuplja: ponovo pokrenuti živu instancu ili duže čekati na otkazalu.

Pad procesa je teško pouzdano [[Razlikovanje pada procesa, usporenja i prekida mreže|razlikovati]] od veoma sporog procesa, kao što opisuje beleška [[Pad procesa]], pa greške detekcije nisu samo posledica loše izabranih vrednosti.

Opažanja mogu da potiču iz [[Provera zdravlja servisne instance|provera zdravlja]], [[Signal života|signala života]], [[Metrika|metrika]], [[Log|logova]] i [[Trag|tragova]]. Veća [[Opservabilnost|opservabilnost]] poboljšava osnovu za odluku, ali ne garantuje da će odluka biti tačna.

Vreme potrebno za detekciju ulazi u ostvareno trajanje oporavka, a to trajanje se poredi sa [[Ciljno vreme oporavka|ciljnim vremenom oporavka]]. Ako funkcija stane u 12:00, a prekid bude primećen u 12:02, od cilja od 10 minuta već su potrošena dva.
