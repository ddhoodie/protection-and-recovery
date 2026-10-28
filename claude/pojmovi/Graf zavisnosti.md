---
tip: pojam
aliases: [dependency graph, service dependency graph]
izvor: "Amazon CloudWatch Application Signals API Reference, DependencyGraph, https://docs.aws.amazon.com/applicationsignals/latest/APIReference/API_DependencyGraph.html"
---
# Graf zavisnosti (dependency graph)

## Definicija

Graf zavisnosti jeste usmerena struktura u kojoj čvorovi predstavljaju [[Aplikativni servis|aplikativne servise]], a grana od jednog čvora ka drugom predstavlja [[Zavisnost servisa|zavisnost prvog servisa od drugog]].

## Primer

U poslovnom toku primarnog [[Aplikativni sistem|aplikativnog sistema]], tri servisa označimo sa A, B i C. Ako A za svoju funkciju zahteva rezultat servisa B, a B rezultat servisa C, graf sadrži grane `A → B` i `B → C`. Put od A do C pokazuje da A posredno zavisi od C, pa [[Otkaz komponente distribuiranog sistema|otkaz]] servisa C može sprečiti završetak funkcija servisa B i A. Graf pokazuje redosled funkcionalnih preduslova: B ne može potpuno da izvršava funkciju koja zavisi od C dok C nije spreman, a isto važi za A u odnosu na B. Pokretanje, konfigurisanje i nezavisne provere servisa mogu se obavljati paralelno. Sve [[Servisna instanca|servisne instance]] jednog logičkog servisa predstavljene su istim čvorom.

## Napomene

Graf zavisnosti je apstraktna struktura, dok je dijagram ili mapa servisa njen vizuelni prikaz. Smer grane prati konvenciju iz beleške [[Zavisnost servisa]]: `A → B` znači da A zavisi od B.

Graf mora imati određen obim i trenutak važenja. Projektovani graf opisuje nameravanu arhitekturu, dok graf izveden iz telemetrije opisuje samo zavisnosti opažene u posmatranom periodu. Graf ne mora biti acikličan; uzajamne zavisnosti stvaraju ciklus i mogu onemogućiti jednostavan redosled oporavka.
