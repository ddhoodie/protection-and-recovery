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

Otkrivanje otkaza primarnog čvora jeste postupak u kojem se, na osnovu izostalih ili neispravnih odgovora u utvrđenoj vremenskoj granici i dodatnih opažanja o stanju čvora, zaključuje da je [[Primarni čvor|primarni čvor]] doživeo [[Otkaz komponente distribuiranog sistema|otkaz]] i procenjuje da li su njegovi procesi doživeli [[Pad procesa|pad]] ili se i dalje izvršavaju, ali odgovaraju izvan vremenske granice.

## Primer

U primarnom cloud kontekstu, nadzorna komponenta šalje primarnom čvoru P proveru svake 2 sekunde i očekuje odgovor u roku od jedne sekunde. U 12:00:00 P prestane da odgovara. Posle pet uzastopnih provera bez odgovora, u 12:00:10, nadzorna komponenta zaključuje da je P otkazao. Sam izostanak odgovora isto izgleda i kada je P pao, i kada je preopterećen, i kada je prekinuta mreža između nadzorne komponente i čvora P.

Zato nadzorna komponenta proverava dodatne signale. Ako poruke replikacije više ne stižu ni do replike R1 ni do replike R2, a cloud platforma prijavljuje da je virtuelna mašina čvora P zaustavljena, zaključak o padu je osnovan. Ako R1 i dalje prima poruke replikacije od čvora P, a platforma prijavljuje da virtuelna mašina radi uz procesor opterećen 100%, P je usporen, a ne pao. [[Servisna instanca|Servisne instance]] koje u tom periodu pokušavaju upis dobijaju greške ili čekaju, pa vreme otkrivanja ulazi u [[Ciljno vreme oporavka|RTO]].

## Napomene

Rezultat otkrivanja je zaključak, a ne pouzdano utvrđena činjenica. Moguće su dve vrste greške. Lažno otkrivanje proglašava ispravan čvor neispravnim i može dovesti do nepotrebnog failover-a. Zakasnelo otkrivanje ostavlja sistem bez prijema upisa duže nego što je potrebno i troši RTO. Vremenska granica i broj uzastopnih neuspelih provera određuju odnos između ove dve greške.

Razlika između pada i usporenja ovde je važnija nego kod obične servisne instance, zbog onoga što sledi posle [[Failover|failover-a]]. Čvor čiji su procesi pali ne prihvata upise, pa je preuzimanje njegove uloge bezbedno. Usporen čvor nastavlja da radi i, kada se opterećenje smanji, može ponovo da prihvata upise kao da je i dalje primarni. Failover pokrenut zbog usporenja zato vodi u [[Dva istovremena primarna čvora|dva istovremena primarna čvora]] ako stari čvor nije zaustavljen [[Fencing|fencing-om]]. Kod kratkotrajnog usporenja ponekad je bolje sačekati nego menjati primarni čvor.

Dodatna opažanja smanjuju nesigurnost, ali je ne uklanjaju. Usporen čvor može ubrzo zaista da padne, a podatak platforme o stanju virtuelne mašine može da kasni. Više nezavisnih posmatrača, na primer nadzorna komponenta i replike R1 i R2, smanjuje rizik da se problem na jednoj mrežnoj putanji protumači kao otkaz čvora, ali failover i dalje mora biti bezbedan i kada je zaključak pogrešan.

Otkrivanje daje samo zaključak o stanju čvora. Odluka da se zbog tog zaključka promeni primarni čvor je [[Pokretanje failover-a|pokretanje failover-a]]. Ovaj pojam je poseban slučaj [[Detekcija otkaza|detekcije otkaza]] i [[Razlikovanje pada procesa, usporenja i prekida mreže|razlikovanja pada procesa, usporenja i prekida mreže]], primenjen na komponentu od koje zavisi prijem upisa u repliciranu bazu.
