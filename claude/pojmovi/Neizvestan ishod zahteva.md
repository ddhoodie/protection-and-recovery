---
tip: pojam
aliases: [uncertain request outcome, indeterminate outcome]
izvor: "Peter Bailis i Kyle Kingsbury, The Network Is Reliable, Communications of the ACM, 57(9), 2014, str. 48-55, https://doi.org/10.1145/2643130"
---
# Neizvestan ishod zahteva (uncertain request outcome)

## Definicija

Neizvestan ishod zahteva jeste stanje u kojem komponenta [[Distribuirani sistem|distribuiranog sistema]] koja je poslala zahtev nije dobila odgovor, pa ne može da zna da li zahtev nije stigao do primaoca, da li ga je primalac primio i nije izvršio, ili ga je izvršio, a odgovor se izgubio.

## Primer

U primarnom cloud kontekstu, servis A u okviru [[Poslovni tok kroz više servisa i baza|poslovnog toka]] šalje servisu B zahtev da izvrši korak toka. U tom trenutku nastane [[Mrežna particija|mrežna particija]] i [[Rok čekanja|rok čekanja]] servisa A istekne. Servis B je možda izvršio korak i upisao izmenu na primarni čvor, a možda zahtev nije ni primio. Ako servis A pošalje isti zahtev ponovo, korak može da bude izvršen dva puta. Ako tok proglasi neuspelim i odustane, u servisu B može da ostane izvršen korak koji niko ne prati, pa je tok u nekonzistentnom stanju.

## Napomene

Istek roka čekanja određuje kada komponenta prestaje da čeka, a neizvestan ishod opisuje šta ona posle toga zna o zahtevu. Duže čekanje ne otklanja neizvesnost, jer odgovor možda nikada neće stići.

Mrežna particija je čest uzrok, ali isto stanje nastaje i kada primalac doživi [[Pad procesa|pad procesa]] ili [[Usporavanje servisa|usporavanje]]. Pošiljalac na osnovu izostanka odgovora ne može da zna koji je slučaj u pitanju.

Neizvesnost se razrešava tek naknadno. Pošiljalac može da pita primaoca kakav je ishod zahteva kada veza bude ponovo uspostavljena, ili da zahtev ponovi na način koji ne izaziva dupli efekat ako je zahtev već izvršen. Zahtevi sa neizvesnim ishodom zato su deo [[Oporavak posle mrežne particije|oporavka posle mrežne particije]].

Isto važi za upis u bazu. Ako servisna instanca ne dobije potvrdu izmene od primarnog čvora, izmena je možda trajno sačuvana, a možda nije.
