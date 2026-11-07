---
noteId: "49efb6f0d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "new primary selection"
  - "leader election"
  - "primary election"
izvor: "Microsoft, Failover and failback, https://learn.microsoft.com/en-us/azure/reliability/concept-failover-failback; Diego Ongaro i John Ousterhout, In Search of an Understandable Consensus Algorithm, USENIX ATC 2014, https://raft.github.io/raft.pdf"

---

# Izbor novog primarnog čvora (new primary selection, leader election)

## Definicija

Izbor novog primarnog čvora jeste postupak kojim se među [[Replika|replikama]] određuje čvor koji će preuzeti ulogu [[Primarni čvor|primarnog čvora]], tako da u jednom izboru bude izabran najviše jedan čvor i da se uzme u obzir koliko je koja replika ažurna.

## Primer

U primarnom cloud kontekstu, posle otkaza primarnog čvora P replika R1 ima promene do 11:59:58, a replika R2 do 11:59:40. Ako se izabere R1, gube se promene iz poslednje dve sekunde pre otkaza, a ako se izabere R2, gubi se 20 sekundi promena. Za [[Ciljna tačka oporavka|RPO]] od pet minuta obe mogućnosti su prihvatljive, ali se bira R1 jer se njome gubi manje podataka. Posle izbora R2 ostaje replika, ali sada prima promene od R1. Kada bi i R1 i R2 istovremeno zaključile da su izabrane, nastala bi [[Dva istovremena primarna čvora|dva istovremena primarna čvora]], zbog čega izbor mora da odredi najviše jedan čvor.

## Napomene

Izbor može da sprovede jedna nadzorna komponenta ili sami čvorovi glasanjem. Kod glasanja čvor postaje primarni samo ako dobije glasove većine, a svaki čvor u jednom izboru glasa samo jednom, pa dva kandidata ne mogu istovremeno imati većinu. Ako postoje samo dva čvora bez posrednika, nijedan ne može da razlikuje otkaz drugog od [[Prekid mreže|prekida mreže]] između njih, pa se za izbor većinom koristi bar tri učesnika.

Ažurnost nije jedini kriterijum. Na izbor mogu uticati i lokacija i kapacitet replike, zbog čega najažurnija replika ne mora uvek biti izabrana.

Izbor može da ne uspe ako nijedna replika nije dostupna, ako sve previše zaostaju ili ako nijedan kandidat ne dobije većinu. U tom slučaju izbor se ponavlja, a vreme bez primarnog čvora troši [[Ciljno vreme oporavka|RTO]]. Ako se ne izabere nijedan čvor, failover postaje [[Neuspeli failover|neuspeli failover]].
