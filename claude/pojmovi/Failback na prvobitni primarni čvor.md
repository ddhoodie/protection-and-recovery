---
noteId: "4a858e50d55111f1ae0e01469be8825c"
tags: []
tip: "pojam"
aliases:
  - "failback"
izvor: "Microsoft, Failover and failback, https://learn.microsoft.com/en-us/azure/reliability/concept-failover-failback"

---

# Failback na prvobitni primarni čvor (failback)

## Definicija

Failback na prvobitni primarni čvor jeste postupak kojim se, posle [[Failover|failover-a]], uloga [[Primarni čvor|primarnog čvora]] i zahtevi za upis vraćaju na prvobitni čvor, nakon što je on popravljen i usklađen sa trenutnim primarnim čvorom.

## Primer

U primarnom cloud kontekstu, posle failover-a u 12:00 replika R1 radi kao primarni čvor. Čvor P se popravi u 14:00, ali ne može odmah da preuzme ulogu, jer nema promene koje je R1 prihvatio u međuvremenu, a ima upise iz poslednje dve sekunde pre otkaza koje nije stigao da replicira. Te upise mora da odbaci ili posebno sačuva za proveru, a zatim počinje da radi kao [[Replika|replika]] čvora R1 i sustiže ga. Kada P sustigne R1, u planiranom terminu u 22:00 R1 prestaje da prihvata upise, adresa za upis se preusmerava na P i P ponovo postaje primarni čvor.

## Napomene

Failback nije obavezan, jer sistem može trajno ostati na novom primarnom čvoru. Izvodi se kada za to postoji razlog, na primer kada je prvobitni čvor na povoljnijoj lokaciji ili ima veći kapacitet.

Failback je nova promena uloge, pa nosi iste rizike kao failover: [[Dva istovremena primarna čvora|dva istovremena primarna čvora]] i gubitak upisa ako trenutni primarni čvor prestane sa radom pre nego što su sve njegove promene stigle na prvobitni. Za razliku od failover-a, failback se planira, pa se može izvesti bez gubitka podataka: trenutni primarni čvor prvo prestane da prihvata upise, sačeka se da prvobitni čvor primi sve promene, i tek tada se upisi preusmeravaju. Cena je kratak prekid prijema upisa.

Upisi koje je prvobitni primarni čvor prihvatio, a nije stigao da replicira, mogli su biti potvrđeni klijentima. Zato ih ne treba ni prećutno odbaciti ni nekontrolisano vratiti u bazu, već sačuvati i uskladiti sa trenutnim stanjem.
