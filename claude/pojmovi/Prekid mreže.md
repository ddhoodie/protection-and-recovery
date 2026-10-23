---
tip: pojam
aliases: [network outage, network interruption, network communication failure]
izvor: "George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, odeljak 2.3.2, https://www.pearson.com/en-us/subject-catalog/p/distributed-systems-concepts-and-design/P200000003160/9780132143011"
---
# Prekid mreže (network outage)

## Definicija

Prekid mreže jeste stanje u kojem jedan ili više mrežnih komunikacionih puteva između komponenti [[Distribuirani sistem|distribuiranog sistema]] prestanu da prenose poruke, dok procesi na njihovim krajevima mogu nastaviti da se izvršavaju.

## Primer

U primarnom cloud kontekstu, prekid komunikacionog puta između instanci servisa A i B spreči prenos zahteva i odgovora. Obe [[Servisna instanca|servisne instance]] nastavljaju lokalno da izvršavaju svoje procese, ali servis A više ne može da koristi [[Zavisnost servisa|funkciju od koje zavisi]] kod servisa B. Izostanak odgovora iz perspektive servisa A izgleda isto kao da je proces servisa B pao, iako se on i dalje izvršava.

## Napomene

Prekid može zahvatiti jedan smer, jedan komunikacioni put, određeni par komponenti ili veći deo mreže. Kada prekid podeli komponente u grupe koje mogu da komuniciraju unutar grupe, ali ne i između grupa, nastaje mrežna particija.

Pojedinačno izgubljena poruka nije nužno prekid mreže. Povremeni gubici mogu biti prikriveni ponovnim slanjem, dok prekid označava stanje u kojem potrebna razmena poruka nije moguća. Veoma spora isporuka bez prestanka prenosa bliža je [[Usporavanje servisa|usporavanju]] ili otkazu po vremenu odziva.

Prekid mreže se razlikuje od [[Pad procesa|pada procesa]] jer krajnji procesi mogu ostati ispravni. Udaljena komponenta koja vidi samo izostanak odgovora ne može bez dodatnih pretpostavki pouzdano utvrditi koji je događaj nastao.
