---
noteId: "4a3ee860d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "node fencing"
  - "fencing token"
  - "STONITH"
izvor: "Martin Kleppmann, How to do distributed locking, 2016, https://martin.kleppmann.com/2016/02/08/how-to-do-distributed-locking.html; PostgreSQL Documentation, odeljak 26.3 Failover, https://www.postgresql.org/docs/current/warm-standby-failover.html"

---

# Fencing

## Definicija

Fencing jeste mera kojom se čvoru koji više ne sme da ima ulogu [[Primarni čvor|primarnog čvora]] spolja onemogućava da menja podatke, isključivanjem tog čvora, blokiranjem njegovog pristupa ili odbijanjem njegovih upisa, bez oslanjanja na njegovu saradnju.

## Primer

U primarnom cloud kontekstu, nadzorna komponenta je zaključila da je primarni čvor P otkazao, ali ne može da isključi mogućnost da je P samo usporen. Pre nego što replika R1 počne da prihvata upise, nadzorna komponenta preko cloud API-ja ugasi virtuelnu mašinu čvora P i sačeka potvrdu da je ugašena. Tek tada R1 preuzima ulogu. To je varijanta poznata kao STONITH. U varijanti sa tokenom, svaki novi primarni čvor dobija veći broj: P je imao token 33, a R1 dobija 34. Skladište podataka koje proverava tokene već je primilo upis sa tokenom 34, pa odbija zakasneli upis čvora P sa tokenom 33.

## Napomene

Fencing je potreban jer čvor koji je samo usporen ili odsečen ne mora znati da je izgubio ulogu. Zato se bezbednost [[Failover|failover-a]] ne oslanja na to da će se taj čvor sam povući, čime se sprečava [[Split-brain|split-brain]].

Redosled je bitan. Fencing mora da se završi pre nego što novi primarni čvor počne da prihvata upise, jer u suprotnom postoji interval u kojem oba čvora mogu da upisuju. Ako fencing ne uspe, na primer zato što cloud API nije dostupan, bezbednije je odložiti failover nego rizikovati [[Dva istovremena primarna čvora|dva istovremena primarna čvora]], iako se time produžava ostvareno trajanje oporavka i smanjuje preostalo vreme do granice [[Ciljno vreme oporavka|RTO-a]].

Načini se razlikuju po tome gde deluju. Isključivanje čvora zaustavlja ceo čvor, blokiranje pristupa mu oduzima mrežnu vezu ili pravo pristupa skladištu, a odbijanje upisa pomoću tokena zahteva da sam resurs proverava token i pamti najveći primljeni.
