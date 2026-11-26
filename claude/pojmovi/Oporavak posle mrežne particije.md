---
tip: pojam
aliases: [partition recovery, izlečenje particije, partition healing]
izvor: "Eric Brewer, CAP Twelve Years Later: How the \"Rules\" Have Changed, IEEE Computer, 45(2), 2012, str. 23-29"
---
# Oporavak posle mrežne particije (partition recovery)

## Definicija

Oporavak posle mrežne particije jeste postupak koji počinje kada se komunikacija između grupa komponenti razdvojenih [[Mrežna particija|mrežnom particijom]] ponovo uspostavi i završava se kada svi čvorovi baze podataka priznaju isti primarni čvor, kada su izmene nastale na razdvojenim stranama odbačene, spojene ili ručno usklađene, kada je za svaki zahtev čiji je ishod ostao [[Neizvestan ishod zahteva|neizvestan]] utvrđeno da li je izvršen i kada je svaki tok zaustavljen tokom particije nastavljen ili poništen.

## Primer

U primarnom cloud kontekstu, particija je od 12:00 do 12:06 odvajala zonu 1, u kojoj su primarni čvor P i servis A, od zona 2 i 3. U međuvremenu je R1 postao primarni čvor. U 12:06 veza se vraća. Najpre P utvrđuje da više nije primarni čvor i [[Ponovno priključivanje bivšeg primarnog čvora|ponovo se priključuje]] kao replika čvora R1. Zatim servis A, za svaki zahtev servisu B čiji je ishod ostao [[Neizvestan ishod zahteva|neizvestan]], pita servis B da li je korak izvršen. Servis B prolazi kroz spisak tokova koje je zabeležio u [[Režim rada tokom particije|režimu rada tokom particije]] i nastavlja ih. Tek kada je spisak prazan, servis B izlazi iz režima rada tokom particije. Oporavak je završen u 12:14, iako je mreža ispravna od 12:06.

## Napomene

Ponovno uspostavljanje veze (izlečenje particije, partition healing) samo je početak oporavka. Sistem u kojem je mreža ispravna i dalje može da ima čvor koji veruje da je primarni, nepomirene izmene posle [[Split-brain|split-brain-a]] ili tokove zaustavljene na pola.

Redosled koraka je bitan. Uloge čvorova se usklađuju pre podataka, a podaci pre tokova, jer se tok ne može ispravno nastaviti dok se ne zna koja verzija podataka važi.

Veza koja se vrati, pa ponovo prekine, može da prekine oporavak usred postupka. Zato se oporavak često pokreće tek kada je veza stabilna određeno vreme, a koraci oporavka moraju moći da se bezbedno ponove.

Uspešnost oporavka se meri kao [[Ukupno vreme oporavka sistema|ukupno vreme oporavka sistema]] i [[Broj tokova u nekonzistentnom stanju|broj tokova u nekonzistentnom stanju]] posle izlečenja particije.
