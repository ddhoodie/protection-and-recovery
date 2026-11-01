---
tip: pojam
aliases: [trace, traces, distributed trace, tragovi]
izvor: "OpenTelemetry Specification, Overview, odeljci Tracing Signal, Traces i Spans, https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/overview.md"
---
# Trag (trace)

## Definicija

Trag jeste skup međusobno povezanih opisa operacija, sa vremenom početka i završetka svake operacije, kojima komponente [[Distribuirani sistem|distribuiranog sistema]] obrađuju jedan zahtev ili drugu logičku operaciju.

## Primer

U primarnom cloud kontekstu, jedan zahtev u okviru [[Poslovni tok kroz više servisa i baza|poslovnog toka]] stiže do servisa A, koji ima [[Zavisnost servisa|zavisnost]] od servisa B, a servis B upisuje podatke na primarni čvor replicirane baze. Trag tog zahteva sadrži ove operacije, od kojih svaka obuhvata narednu:

- obrada zahteva u servisu A: 2.450 ms
- poziv servisa B iz servisa A: 2.430 ms
- obrada zahteva u servisu B: 2.400 ms
- upis u bazu iz servisa B: 2.100 ms

Iz ovih trajanja vidi se da je za ovaj zahtev upis trajao 2.100 ms od ukupno 2.450 ms, pa kašnjenje najvećim delom nastaje za vreme upisa. Trajanje upisa izmereno iz servisa B ne pokazuje koliko je vremena potrošeno na obradu u bazi, čekanje na resurse ili komunikaciju sa čvorom, niti zašto je upis trajao toliko.

## Napomene

Opis jedne operacije u tragu naziva se raspon (span).

Trag pokazuje kako je vreme raspoređeno unutar jednog zahteva, [[Metrika|metrika]] kako se neka veličina menja kroz vreme, a [[Log|log]] šta je komponenta zabeležila o pojedinačnim događajima. Zato metrika može da pokaže da su odgovori uopšte sporiji, a trag gde je vreme potrošeno u konkretnom zahtevu.

Trag jednog zahteva ne mora da predstavlja ponašanje celog sistema. Taj zahtev može biti netipičan, a sistemi za prikupljanje tragova mogu da čuvaju samo uzorak zahteva. Ako se čuva jedan od sto tragova, spor zahtev može da ostane nesačuvan, pa metrika pokazuje sporost, a dostupni trag brz zahtev.

Trag sam po sebi ne dokazuje uzrok problema. On pokazuje gde je vreme potrošeno, a duga operacija može biti i posledica čekanja na nešto što trag ne prikazuje.

Trag doprinosi [[Opservabilnost|opservabilnosti]] samo ako ga komponente na putu zahteva održavaju. Ako komponenta ne prosledi podatke o tragu ili ne zabeleži svoju operaciju, trag ostaje nepotpun, pa izostanak operacije u njemu ne dokazuje da ona nije izvršena.
