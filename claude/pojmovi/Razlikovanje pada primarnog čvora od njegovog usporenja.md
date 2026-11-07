---
noteId: "49a2cf70d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "distinguishing primary crash from slowdown"
izvor: "George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, odeljak 2.3.2, https://www.pearson.com/en-us/subject-catalog/p/distributed-systems-concepts-and-design/P200000003160/9780132143011"

---

# Razlikovanje pada primarnog čvora od njegovog usporenja (distinguishing primary crash from slowdown)

## Definicija

Razlikovanje pada primarnog čvora od njegovog usporenja jeste utvrđivanje, na osnovu opažanja dodatnih u odnosu na izostanak odgovora, da li su procesi [[Primarni čvor|primarnog čvora]] doživeli [[Pad procesa|pad]] ili se i dalje izvršavaju, ali odgovaraju izvan vremenske granice.

## Primer

U primarnom cloud kontekstu, servis A u 12:00 prestane da dobija odgovore od primarnog čvora P. Nadzorna komponenta zatim proverava dodatne signale: replika R1 i dalje prima poruke replikacije od čvora P, a cloud platforma prijavljuje da virtuelna mašina čvora P radi, uz procesor opterećen 100%. Ti podaci ukazuju na usporenje čvora P, a ne na pad. Da su poruke replikacije prestale da stižu i do R1 i do R2, a platforma prijavila da je virtuelna mašina zaustavljena, zaključak o padu bio bi osnovaniji.

## Napomene

Razlikovanje je važno zbog onoga što sledi posle [[Failover|failover-a]]. Čvor čiji su procesi pali ne prihvata upise, pa je preuzimanje njegove uloge bezbedno. Usporen čvor nastavlja da radi i, kada se opterećenje smanji, može ponovo da prihvata upise kao da je i dalje primarni. Failover pokrenut zbog usporenja zato vodi u [[Dva istovremena primarna čvora|dva istovremena primarna čvora]] ako stari čvor nije zaustavljen [[Fencing|fencing-om]]. Kod kratkotrajnog usporenja ponekad je bolje sačekati nego menjati primarni čvor.

Dodatna opažanja smanjuju nesigurnost, ali je ne uklanjaju. Usporen čvor može ubrzo zaista da padne, a podatak platforme o stanju virtuelne mašine može da kasni. Udaljena komponenta koja vidi samo izostanak odgovora ne može bez dodatnih pretpostavki pouzdano utvrditi šta se dogodilo, pa failover mora biti bezbedan i kada je zaključak pogrešan.

[[Usporavanje servisa]] opisuje ponašanje funkcije servisa, dok se ovde posmatra jedan čvor baze. Slučaj [[Prekid mreže|prekida mreže]] obrađuje se u celini o detekciji otkaza.
