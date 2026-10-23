---
tip: pojam
aliases: [potpuni pad sistema, total system failure, complete system outage]
izvor: "ISO/IEC/IEEE 24765:2017, Systems and software engineering - Vocabulary, odeljak 3.1560, https://www.iso.org/standard/71952.html"
---
# Potpuni otkaz sistema (total system failure)

## Definicija

Potpuni otkaz sistema jeste stanje nastalo kada [[Distribuirani sistem|distribuirani sistem]] prestane da na svojoj granici pruža bilo koju od svojih zahtevanih funkcija, nezavisno od toga da li pojedine unutrašnje komponente i dalje funkcionišu.

## Primer

U primarnom cloud kontekstu, balanser predstavlja jedinu pristupnu tačku ka [[Servisna instanca|servisnim instancama]]. Ako balanser doživi [[Otkaz komponente distribuiranog sistema|otkaz]], korisnici više ne mogu da pristupe nijednoj funkciji sistema, iako servisne instance i replicirana baza nastavljaju da rade. Sa stanovišta unutrašnje strukture otkazala je samo jedna komponenta, ali je na granici sistema nastao potpuni otkaz.

## Napomene

Potpunost se odnosi na gubitak svih zahtevanih funkcija na granici posmatranog sistema, a ne na broj njegovih unutrašnjih komponenti koje su otkazale. Interna funkcija koju korisnik ne može da dobije preko granice sistema ne sprečava klasifikaciju događaja kao potpunog otkaza.

[[Delimični otkaz]] i potpuni otkaz sistema nisu strogo suprotna stanja jer opisuju različite nivoe. Incident može biti delimičan prema broju komponenti koje su otkazale, a istovremeno potpun prema funkcijama koje sistem pruža. Nasuprot tome, otkaz komponente koji je uspešno prikriven ne mora da izazove potpuni otkaz sistema.
