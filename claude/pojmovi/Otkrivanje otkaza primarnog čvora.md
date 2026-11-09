---
noteId: "49855c60d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "primary failure detection"
  - "primary node failure detection"
  - "distinguishing primary crash from slowdown"
izvor: "PostgreSQL Documentation, odeljak 26.3 Failover, https://www.postgresql.org/docs/current/warm-standby-failover.html; George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, odeljak 2.3.2, https://www.pearson.com/en-us/subject-catalog/p/distributed-systems-concepts-and-design/P200000003160/9780132143011"
---

# Otkrivanje otkaza primarnog čvora (primary failure detection)

## Definicija

Otkrivanje otkaza primarnog čvora jeste postupak u kojem se, na osnovu izostalih ili neispravnih odgovora u utvrđenoj vremenskoj granici i dodatnih opažanja o stanju čvora, procenjuje da li izostanak odgovora potiče od [[Pad procesa|pada]] procesa [[Primarni čvor|primarnog čvora]], njegovog [[Usporavanje servisa|usporenja]] ili [[Prekid mreže|prekida mreže]], i na osnovu toga zaključuje da li je primarni čvor doživeo [[Otkaz komponente distribuiranog sistema|otkaz]].

## Primer

U primarnom cloud kontekstu, nadzorna komponenta šalje primarnom čvoru P proveru svake 2 sekunde i očekuje odgovor u [[Rok čekanja|roku čekanja]] od jedne sekunde. U 12:00:00 P prestane da odgovara. Posle pet uzastopnih provera bez odgovora, u 12:00:10, nadzorna komponenta zna samo da odgovori izostaju. Taj izostanak isto izgleda i kada je P pao, i kada je preopterećen, i kada je prekinuta mreža između nadzorne komponente i čvora P.

Zato nadzorna komponenta proverava dodatne signale:

- Ako poruke replikacije više ne stižu ni do replike R1 ni do replike R2, a cloud platforma prijavljuje da je virtuelna mašina čvora P zaustavljena, zaključak o padu je osnovan.
- Ako R1 i dalje prima poruke replikacije od čvora P, a platforma prijavljuje da virtuelna mašina radi uz procesor opterećen 100%, P je usporen, a ne pao.
- Ako R1 i R2 i dalje primaju poruke replikacije, a platforma prijavljuje da virtuelna mašina radi bez preopterećenja, verovatan je prekid mreže na putanji između nadzorne komponente i čvora P. P tada nije ni pao ni usporen, pa se failover ne pokreće samo na osnovu izostanka odgovora na proveru.

U prva dva slučaja [[Servisna instanca|servisne instance]] koje pokušavaju upis dobijaju greške ili čekaju, pa vreme otkrivanja ulazi u ostvareno trajanje oporavka, koje se poredi sa [[Ciljno vreme oporavka|RTO-om]].

## Napomene

Rezultat otkrivanja je zaključak, a ne pouzdano utvrđena činjenica. Moguće su dve vrste greške. Lažno otkrivanje proglašava ispravan čvor neispravnim i može dovesti do nepotrebnog failover-a. Zakasnelo otkrivanje ostavlja sistem bez prijema upisa duže nego što je potrebno, čime produžava ostvareno trajanje oporavka i smanjuje preostalo vreme do granice RTO-a. Vremenska granica i broj uzastopnih neuspelih provera određuju odnos između ove dve greške.

Razlika između pada, usporenja i prekida mreže ovde je važnija nego kod obične servisne instance, zbog onoga što sledi posle [[Failover|failover-a]]. Čvor čiji su procesi pali ne prihvata upise, pa je preuzimanje njegove uloge bezbedno. Usporen čvor nastavlja da radi i, kada se opterećenje smanji, može ponovo da prihvata upise kao da je i dalje primarni. Čvor odsečen samo od nadzorne komponente radi ispravno sve vreme i nastavlja da prima upise od servisnih instanci koje do njega i dalje dopiru. Failover pokrenut zbog usporenja ili prekida mreže zato vodi u [[Dva istovremena primarna čvora|dva istovremena primarna čvora]] ako stari čvor nije zaustavljen [[Fencing|fencing-om]]. Kod kratkotrajnog usporenja ponekad je bolje sačekati nego menjati primarni čvor.

Dodatna opažanja smanjuju nesigurnost, ali je ne uklanjaju. Usporen čvor može ubrzo zaista da padne, a podatak platforme o stanju virtuelne mašine može da kasni. Više nezavisnih posmatrača, na primer nadzorna komponenta i replike R1 i R2, smanjuje rizik da se problem na jednoj mrežnoj putanji protumači kao otkaz čvora, ali failover i dalje mora biti bezbedan i kada je zaključak pogrešan.

Otkrivanje daje samo zaključak o stanju čvora. Odluka da se zbog tog zaključka promeni primarni čvor je [[Pokretanje failover-a|pokretanje failover-a]]. Ovaj pojam je poseban slučaj [[Detekcija otkaza|detekcije otkaza]] i [[Razlikovanje pada procesa, usporenja i prekida mreže|razlikovanja pada procesa, usporenja i prekida mreže]], primenjen na komponentu od koje zavisi prijem upisa u repliciranu bazu.
