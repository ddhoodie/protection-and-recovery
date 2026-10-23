---
tip: pojam
aliases: [component failure, distributed system component failure]
izvor: "Algirdas Avižienis, Jean-Claude Laprie, Brian Randell i Carl Landwehr, Basic Concepts and Taxonomy of Dependable and Secure Computing, IEEE Transactions on Dependable and Secure Computing, 1(1), 2004, odeljak 2.2, https://doi.org/10.1109/TDSC.2004.2"
---
# Otkaz komponente distribuiranog sistema (component failure)

## Definicija

Otkaz komponente distribuiranog sistema jeste događaj u kojem hardverska ili softverska komponenta unutar [[Distribuirani sistem|distribuiranog sistema]] prestaje da na svojoj granici pruža zahtevanu funkciju ili je pruža izvan utvrđenih granica ispravnosti, bez obzira na uzrok i na to da li je zbog toga nastao [[Potpuni otkaz sistema|potpuni otkaz sistema]].

## Primer

U primarnom cloud kontekstu, jedna [[Servisna instanca|servisna instanca]] prestane da odgovara na zahteve u dozvoljenom vremenu. Na granici te instance više se ne dobija zahtevana funkcija, pa je instanca otkazala čak i ako njen proces još postoji. Balanser može da usmeri nove zahteve na druge instance, zbog čega otkaz ove komponente ne mora da postane otkaz celog [[Aplikativni sistem|aplikativnog sistema]].

## Napomene

Otkaz se određuje u odnosu na granicu posmatrane komponente i zahtevano ponašanje na toj granici. Isto stanje može zato biti otkaz jedne komponente, a samo unutrašnji poremećaj šireg sistema koji ga uspešno prikriva.

Uzrok otkaza, neispravno unutrašnje stanje i sam otkaz nisu isto. Uzrok može dovesti komponentu u neispravno stanje, a ono zatim može, ali ne mora, postati spolja uočljiv otkaz. Otkaz jedne komponente može preko [[Zavisnost servisa|zavisnosti servisa]] sprečiti funkciju drugih komponenti ili ostati izolovan redundansom.

Otkaz komponente i potpuni otkaz sistema razlikuju se po granici posmatranja. Prvi opisuje događaj na granici jedne komponente, a drugi stanje na granici celog sistema u kojem nije dostupna nijedna zahtevana funkcija. Otkaz komponente može biti prikriven, može umanjiti samo deo funkcionalnosti ili može izazvati potpuni otkaz ako je komponenta [[Jedinstvena tačka otkaza|jedinstvena tačka otkaza]]. Potpuni otkaz sistema takođe može nastati tek kombinacijom više pojedinačnih otkaza.
