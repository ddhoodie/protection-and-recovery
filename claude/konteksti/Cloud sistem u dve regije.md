---
tip: kontekst
uloga: sekundarni
---
# Cloud sistem u dve regije

Poslovni sistem iz primarnog konteksta [[Cloud sistem za oporavak]], postavljen u dve regije, kako bi se pokazali modeli replikacije u kojima upise prima više čvorova replicirane baze. Primarni kontekst opisuje model u kome upise prima samo jedan čvor, pa ga za te modele ne možemo koristiti.

## Elementi

- Dve regije, Regija 1 i Regija 2. Veza između regija je sporija od veze unutar regije i može da se prekine. [[Prekid mreže|Prekid]] te veze deli sistem u dve grupe, pa je to [[Mrežna particija|mrežna particija]].
- [[Aplikativni servis|Aplikativni servisi]] A, B i C, isti kao u primarnom kontekstu, sa [[Servisna instanca|servisnim instancama]] u obe regije.
- Četiri [[Čvor replicirane baze|čvora replicirane baze]]: N1 i N2 u Regiji 1, N3 i N4 u Regiji 2. Oznake N1 do N4 namerno se razlikuju od oznaka P, R1 i R2 iz primarnog konteksta.
- [[Poslovni tok kroz više servisa i baza|Poslovni tok]] koji prolazi kroz servise A, B i C. Njegov status je podatak koji se u primerima replicira.

## Dva modela replikacije

Isti status poslovnog toka može da se replicira na dva alternativna načina. Svaki primer navodi koji model prikazuje, a dva modela se ne mešaju u istom primeru.

- **Model sa više čvorova koji primaju upise (multi-leader).** Sva četiri čvora primaju upise. Servisna instanca upisuje na čvor iz svoje regije, na N1 ili N2 u Regiji 1, odnosno na N3 ili N4 u Regiji 2, a čvor koji je upis primio prosleđuje izmenu ostalim čvorovima.
- **Model bez čvora koji određuje redosled upisa (leaderless).** Status poslovnog toka čuvaju tri čvora, N1, N2 i N3. Čvor N4 ga ne čuva. Servisna instanca šalje upis na sva tri čvora koja čuvaju status, a nijedan čvor ne određuje redosled upisa.

Primeri koji se odnose na replikaciju sa jednim primarnim čvorom ostaju u primarnom kontekstu.
