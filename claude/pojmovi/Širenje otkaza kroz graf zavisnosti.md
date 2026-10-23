---
tip: pojam
aliases: [failure propagation through a dependency graph, failure propagation]
izvor: "AWS Well-Architected Framework, REL05-BP01 - Implement graceful degradation to transform applicable hard dependencies into soft dependencies, https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_mitigate_interaction_failure_graceful_degradation.html"
---
# Širenje otkaza kroz graf zavisnosti (failure propagation through a dependency graph)

## Definicija

Širenje otkaza kroz graf zavisnosti jeste proces u kojem posledica [[Otkaz komponente distribuiranog sistema|otkaza jedne komponente]] onemogući ili degradira zahtevanu funkciju neposredno [[Zavisnost servisa|zavisnog servisa]], koji zatim prenosi posledicu na svoje zavisne servise duž usmerenih puteva u [[Graf zavisnosti|grafu zavisnosti]].

## Primer

U primarnom cloud kontekstu, servis A zavisi od servisa B, a servis B od servisa C, pa graf sadrži grane `A → B` i `B → C`. Kada sve [[Servisna instanca|servisne instance]] servisa C prestanu da pružaju potrebnu funkciju, servis B ne može da završi svoj korak poslovnog toka. Zbog toga ni servis A ne dobija rezultat od B i njegov korak takođe prestaje da napreduje. Posledica početnog otkaza proširila se putem `C → B → A`, suprotno smeru grana koje označavaju zavisnost.

## Napomene

Graf zavisnosti prikazuje moguće puteve širenja, ali sam ne dokazuje da će se otkaz tim putevima proširiti. Ishod zavisi od toga da li je zavisnost neophodna za posmatranu funkciju i da li zavisni servis može da upotrebi zamenski izvor, sačuvanu vrednost, odloženu obradu ili degradirani režim.

Ne širi se fizički događaj koji je izazvao početni otkaz, već njegov funkcionalni uticaj: nedostupnost, kašnjenje ili neispravan rezultat postaju problem za zavisnu komponentu. Kada se tako izazvani otkazi nastavljaju kroz više komponenti, nastaje lančani otkaz.

Više komponenti može otkazati istovremeno zbog zajedničkog uzroka bez širenja kroz njihove međusobne zavisnosti. Da bi se tvrdilo da je došlo do širenja, potrebno je pokazati uzročni put od početnog otkaza kroz konkretne veze zavisnosti.
