---
tip: pojam
aliases: [consistency and availability trade-off during a network partition, CP, AP]
izvor: "Eric Brewer, CAP Twelve Years Later: How the \"Rules\" Have Changed, IEEE Computer, 45(2), 2012, str. 23-29"
---
# Kompromis konzistentnosti i dostupnosti tokom mrežne particije (consistency and availability trade-off during a network partition)

## Definicija

Kompromis konzistentnosti i dostupnosti tokom mrežne particije jeste unapred doneta odluka o tome da li čvorovi [[Replicirana baza u cloud-u|replicirane baze]] tokom [[Mrežna particija|mrežne particije]] odbijaju zahteve koje ne mogu da izvrše uz jaku [[Konzistentnost podataka|konzistentnost podataka]] ili na njih odgovaraju podacima koji mogu da zaostaju za potvrđenim izmenama.

## Primer

U primarnom cloud kontekstu, mrežna particija odvoji [[Replika|replike]] i servis B od [[Primarni čvor|primarnog čvora]]. Servis B čita status [[Poslovni tok kroz više servisa i baza|poslovnog toka]] iz dva razloga. Kada status samo prikazuje, servis B čita sa replike i prihvata da podatak može biti zastareo. Kada na osnovu statusa odlučuje da li da izvrši sledeći korak toka, čita samo sa primarnog čvora, pa tokom particije dobija grešku. Zastareo status bi ga tu mogao navesti da ponovo izvrši već završen korak.

## Napomene

Odluka ne mora biti ista za ceo sistem. Donosi se posebno za svaku vrstu zahteva, prema tome šta je skuplje: odbijen zahtev ili odgovor sa zastarelim podacima.

Sličan izbor postoji i za upise, ali ga ne određuje sam način [[Replikacija podataka sa primarnog čvora na replike|replikacije]]. Kod sinhrone replikacije primarni čvor prestaje da potvrđuje upise kada ne dobije odgovor od podešenog broja replika. Kod asinhrone može da ih potvrđuje i bez odgovora replika, uz rizik da se te izmene izgube ako ulogu primarnog čvora kasnije preuzme drugi čvor.

[[CAP teorema]] kaže da je ovaj izbor neizbežan, a kompromis je odluka kojom se on pravi za konkretan sistem.
