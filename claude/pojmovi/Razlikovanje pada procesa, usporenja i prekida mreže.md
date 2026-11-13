---
tip: pojam
aliases: ["distinguishing process crash, slowdown and network outage", "razlikovanje pada, usporenja i prekida"]
izvor: "Tushar Deepak Chandra i Sam Toueg, Unreliable Failure Detectors for Reliable Distributed Systems, Journal of the ACM, 43(2), 1996, uvod, https://cs.nyu.edu/~apanda/classes/sp25/papers/chandra-toueg.pdf"
---
# Razlikovanje pada procesa, usporenja i prekida mreže (distinguishing process crash, slowdown and network outage)

## Definicija

Razlikovanje pada procesa, usporenja i prekida mreže jeste postupak kojim se, upoređivanjem opažanja iz više izvora i sa više mesta posmatranja, procenjuje da li izostanak ili kašnjenje odgovora potiče od [[Pad procesa|pada procesa]], [[Usporavanje servisa|usporavanja servisa]] ili [[Prekid mreže|prekida mreže]].

## Primer

U primarnom cloud kontekstu, servis A ne dobije odgovor jedne [[Servisna instanca|servisne instance]] servisa B u okviru [[Rok čekanja|roka čekanja]]. Samo iz toga se ne može utvrditi šta se dogodilo, pa se porede druga opažanja:

- Ako odgovori stižu, ali kasno, [[Metrika trajanja odgovora|metrika trajanja odgovora]] raste, a [[Log|log]] instance i dalje dobija nove zapise, to podržava usporavanje.
- Ako servis A ne može da dobije odgovor, a [[Provera zdravlja servisne instance|provera zdravlja]] koju izvodi balanser opterećenja i dalje uspeva, to podržava prekid mreže između servisa A i instance.
- Ako ni servis A ni balanser ne dobijaju odgovor, a novi zapisi i vrednosti metrika prestanu da stižu, to podržava pad procesa.

Treći slučaj ostaje neodređen, jer isto izgleda i kada prekid mreže potpuno odvoji instancu od ostatka sistema, a njen proces i dalje radi.

## Napomene

Sa jednog mesta posmatranja i samo na osnovu izostanka odgovora ova tri slučaja se ne mogu pouzdano razlikovati. Zato je rezultat procena, a ne dokaz, a više mesta posmatranja suzuje moguća objašnjenja, ali ih ne svodi uvek na jedno.

Slučajevi se međusobno ne isključuju. Isti servis može istovremeno da bude usporen i da ima prekid mreže ka jednom pozivaocu, a jedna od njegovih instanci može da doživi pad.

[[Detekcija otkaza]] odlučuje da se komponenta smatra otkazalom, dok razlikovanje procenjuje o kom se slučaju radi. Balanser može da prestane da šalje zahteve instanci i bez te procene, ali izbor sledeće reakcije zavisi od nje: ponovno pokretanje procesa može da pomogne posle pada, ali ne otklanja prekid mreže.

Različite komponente mogu istovremeno da imaju različitu sliku o istom problemu. Provera zdravlja može da uspeva dok pozivaoci ne dobijaju odgovor, pa ishod jednog opažanja ne važi za sve komponente, što ograničava i [[Opservabilnost|opservabilnost]] sistema.
