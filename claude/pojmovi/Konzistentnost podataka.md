---
tip: pojam
aliases: [data consistency, consistency, strong consistency, eventual consistency]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Problems with Replication Lag, i poglavlje 9, odeljak Linearizability"
---
# Konzistentnost podataka (data consistency)

## Definicija

Konzistentnost podataka jeste svojstvo [[Replicirana baza u cloud-u|replicirane baze]] koje određuje koliko podaci vraćeni čitanjem sa bilo kog čvora mogu da zaostaju za izmenama koje je [[Primarni čvor|primarni čvor]] potvrdio.

## Primer

U primarnom cloud kontekstu, servisna instanca servisa A upisuje u [[Replicirana baza u cloud-u|repliciranu bazu]] da je prvi korak [[Poslovni tok kroz više servisa i baza|poslovnog toka]] završen, i [[Primarni čvor|primarni čvor]] potvrđuje upis. Servis B odmah zatim čita status tog toka sa [[Replika|replike]] do koje izmena još nije stigla i dobija stari status, po kojem je prvi korak još u toku. Nekoliko trenutaka kasnije replika primi izmenu i isto čitanje vraća novi status. Baza u ovom primeru je konačno konzistentna: potvrđena izmena postaje vidljiva na svim čvorovima, ali ne odmah.

## Napomene

Najjači nivo je jaka konzistentnost (strong consistency, linearizability): čitanje sa bilo kog čvora uvek vraća sve izmene potvrđene pre njegovog početka, pa se baza ponaša kao da postoji jedna kopija podataka. Slabiji nivo je konačna konzistentnost (eventual consistency): čitanje sa [[Replika|replike]] može vratiti starije podatke, ali ako nema novih izmena, replike posle nekog vremena dostignu primarni čvor. Koji nivo baza pruža zavisi od načina [[Replikacija podataka sa primarnog čvora na replike|replikacije]] i od toga sa kojih čvorova se čita.

Ova beleška ne opisuje konzistentnost u smislu pravila koja podaci moraju da zadovoljavaju, na primer da tok ne sme imati završen korak u jednom servisu, a nezavršen obavezni korak u drugom. To značenje koristi [[Broj tokova u nekonzistentnom stanju]].
