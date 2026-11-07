---
noteId: "49855c60d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "primary failure detection"
  - "primary node failure detection"
izvor: "PostgreSQL Documentation, odeljak 26.3 Failover, https://www.postgresql.org/docs/current/warm-standby-failover.html"
---

# Otkrivanje otkaza primarnog čvora (primary failure detection)

## Definicija

Otkrivanje otkaza primarnog čvora jeste postupak u kojem se, na osnovu izostalih ili neispravnih odgovora u utvrđenoj vremenskoj granici, zaključuje da je [[Primarni čvor|primarni čvor]] doživeo [[Otkaz komponente distribuiranog sistema|otkaz]].

## Primer

U primarnom cloud kontekstu, nadzorna komponenta šalje primarnom čvoru P proveru svake 2 sekunde i očekuje odgovor u roku od jedne sekunde. U 12:00:00 P prestane da odgovara. Posle pet uzastopnih provera bez odgovora, u 12:00:10, nadzorna komponenta zaključuje da je P otkazao. Isti zaključak bi donela i da je P samo preopterećen ili da je prekinuta mreža između nje i čvora P, jer u sva tri slučaja (pad, preopterećenje, prekid mreže) vidi samo izostanak odgovora. [[Servisna instanca|Servisne instance]] koje u tom periodu pokušavaju upis dobijaju greške ili čekaju, pa vreme otkrivanja ulazi u [[Ciljno vreme oporavka|RTO]].

## Napomene

Rezultat otkrivanja je zaključak, a ne pouzdano utvrđena činjenica. Moguće su dve vrste greške. Lažno otkrivanje proglašava ispravan čvor neispravnim i može dovesti do nepotrebnog failover-a i [[Dva istovremena primarna čvora|dva istovremena primarna čvora]]. Zakasnelo otkrivanje ostavlja sistem bez prijema upisa duže nego što je potrebno i troši RTO. Vremenska granica i broj uzastopnih neuspelih provera određuju odnos između ove dve greške. Zbog toga se [[Razlikovanje pada primarnog čvora od njegovog usporenja|razlikovanje pada primarnog čvora od njegovog usporenja]] obrađuje posebno.

Pored izostanka odgovora na provere, signal otkaza mogu biti greške pri upisu koje vide servisne instance ili prestanak poruka replikacije prema replikama. Više nezavisnih posmatrača, na primer nadzorna komponenta i replike R1 i R2, smanjuje rizik da se problem na jednoj mrežnoj putanji protumači kao otkaz čvora.

Otkrivanje daje samo zaključak o stanju čvora. Odluka da se zbog tog zaključka promeni primarni čvor je [[Pokretanje failover-a|pokretanje failover-a]]. Ovaj pojam je poseban slučaj [[Detekcija otkaza|detekcije otkaza]], primenjen na komponentu od koje zavisi prijem upisa u repliciranu bazu.
