---
tip: pojam
aliases: [failure masking, fault masking]
izvor: "Algirdas Avižienis, Jean-Claude Laprie, Brian Randell i Carl Landwehr, Basic Concepts and Taxonomy of Dependable and Secure Computing, IEEE Transactions on Dependable and Secure Computing, 1(1), 2004, https://doi.org/10.1109/TDSC.2004.2"
---
# Maskiranje otkaza (failure masking)

## Definicija

Maskiranje otkaza jeste učinak pri kom je komponenta [[Distribuirani sistem|distribuiranog sistema]] doživela [[Otkaz komponente distribuiranog sistema|otkaz]], a na granici šireg sistema zahtevana funkcija i dalje prolazi jer je druga komponenta obavlja.

## Primer

U primarnom cloud kontekstu, padne [[Pad procesa|proces]] jedne [[Servisna instanca|servisne instance]] servisa B. Balanser šalje zahteve na preostale instance. Korisnik i dalje dobija odgovor. Otkaz instance postoji. Spolja se ne vidi.

Kad padne primarni [[Čvor replicirane baze|čvor replicirane baze]], replike i dalje rade, ali upis staje dok neka replika ne preuzme upise. Tu redundansa nije maskirala otkaz.

## Napomene

[[Delimični otkaz]] znači da je deo komponenti otkazao. Maskiranje znači da se taj otkaz na spoljnoj granici ne vidi. Oporavak je poseban korak: pokvarena instanca i dalje je pokvarena, a njena zamena i dalje traje.
