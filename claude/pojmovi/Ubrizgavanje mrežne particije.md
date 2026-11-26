---
tip: pojam
aliases: [network partition injection, partition testing]
izvor: "Ali Basiri, Niosha Behnam, Ruud de Rooij, Lorin Hochstein, Luke Kosewski, Justin Reynolds i Casey Rosenthal, Chaos Engineering, IEEE Software, 33(3), 2016, str. 35-41, https://doi.org/10.1109/MS.2016.60"
---
# Ubrizgavanje mrežne particije (network partition injection)

## Definicija

Ubrizgavanje mrežne particije jeste namerno i kontrolisano izazivanje [[Mrežna particija|mrežne particije]] ili [[Delimična mrežna particija|delimične mrežne particije]] u [[Distribuirani sistem|distribuiranom sistemu]], radi provere da li se sistem tokom particije i posle nje ponaša onako kako je unapred predviđeno.

## Primer

U primarnom cloud kontekstu, mehanizam za kontrolisano izazivanje otkaza blokira sav saobraćaj između zone 1 i zona 2 i 3 na pet minuta. Pre testa je zapisano šta se očekuje: P prestaje da prihvata upise najkasnije 10 sekundi posle početka, R1 postaje primarni čvor pre isteka [[Ciljno vreme oporavka|RTO-a]], nijedan zapis nema različite izmene na dva čvora, a servis B prelazi u [[Režim rada tokom particije|režim rada tokom particije]]. Posle uklanjanja blokade očekuje se da se P priključi kao replika i da [[Broj tokova u nekonzistentnom stanju|broj tokova u nekonzistentnom stanju]] padne na nulu u roku od 10 minuta. Test pokaže da je P prihvatao upise 40 sekundi, jer je zakup bio pogrešno podešen.

## Napomene

Ubrizgava se uzrok, a ne posledica. Gašenje čvora P nije ubrizgavanje particije, jer P tada ne radi. Kod particije P radi, a samo mu poruke ne stižu, i upravo to otkriva greške u [[Kvorum|kvorumu]], [[Zakup uloge primarnog čvora|zakupu]] i [[Fencing|fencing-u]].

Ubrizgavanje je korisno samo uz unapred zapisana očekivanja i merenje. Bez njih se vidi da je sistem nešto uradio, ali ne i da li je to bilo ispravno.

Treba ubrizgati više vrsta particija: potpunu, delimičnu i jednosmernu, kao i particiju koja se vrati, pa ponovo nastane. Svaka od njih proverava drugu pretpostavku sistema.
