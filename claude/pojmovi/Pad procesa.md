---
tip: pojam
aliases: [process crash, crash failure]
izvor: "George Coulouris, Jean Dollimore, Tim Kindberg i Gordon Blair, Distributed Systems: Concepts and Design, 5. izdanje, odeljak 2.3.2, https://www.pearson.com/en-us/subject-catalog/p/distributed-systems-concepts-and-design/P200000003160/9780132143011"
---
# Pad procesa (process crash)

## Definicija

Pad procesa jeste [[Otkaz komponente distribuiranog sistema|otkaz]] u kojem se tekuće izvršenje procesa neočekivano i nepovratno zaustavlja pre završetka zahtevane funkcije, pa taj proces više ne izvršava programske korake niti učestvuje u razmeni poruka; naknadno pokretanje istog programa predstavlja novo izvršenje.

## Primer

U primarnom cloud kontekstu, kontrolisano izazvan otkaz prekine proces jedne [[Servisna instanca|servisne instance]] dok obrađuje zahtev. Proces više ne izvršava kod niti odgovara na poruke, pa je doživeo pad. Balanser može da usmeri naredne zahteve na druge instance, a pokrenuta zamena ima novi identitet izvršenja i predstavlja novu servisnu instancu.

## Napomene

Pad procesa ne obuhvata proces koji i dalje izvršava, ali je spor, zaglavljen ili nedostupan zbog prekida komunikacije. Međutim, udaljena komponenta koja ne dobija odgovor samo na osnovu tog opažanja ne može pouzdano razlikovati ove slučajeve od pada procesa.

Pad procesa ne znači da je računar na kojem je proces radio otkazao. Gašenje računara može izazvati pad svih procesa na njemu, ali jedan proces može pasti dok računar i drugi procesi nastavljaju da rade. Pad procesa je zato mogući uzrok [[Delimični otkaz|delimičnog otkaza]] distribuiranog sistema.

Model `crash failure` ne pretpostavlja da druge komponente mogu pouzdano da otkriju pad. Jači model `fail-stop` dodatno pretpostavlja da je pad moguće pouzdano detektovati.
