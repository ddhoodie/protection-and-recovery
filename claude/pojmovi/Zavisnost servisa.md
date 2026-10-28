---
tip: pojam
aliases: [service dependency]
izvor: "AWS Well-Architected Framework, REL04-BP01 — Identify the kind of distributed systems you depend on, https://docs.aws.amazon.com/wellarchitected/latest/framework/rel_prevent_interaction_failure_identify.html"
---
# Zavisnost servisa (service dependency)

## Definicija

Zavisnost servisa jeste usmereni odnos u kojem sposobnost jednog [[Aplikativni servis|aplikativnog servisa]] da ispravno izvrši određenu funkciju zavisi od toga da drugi servis pruži potreban podatak ili funkcionalnost pod uslovima koje ta funkcija zahteva.

## Primer

U poslovnom toku primarnog [[Aplikativni sistem|aplikativnog sistema]], jedan servis mora da dobije rezultat drugog servisa pre nego što završi svoj korak. Ako otkažu sve [[Servisna instanca|servisne instance]] drugog servisa, instance prvog mogu ostati pokrenute i odgovarati na proveru zdravlja, ali prvi servis više ne može ispravno da izvrši tu funkciju. [[Otkaz komponente distribuiranog sistema|Otkaz]] se zato može odraziti izvan servisa u kojem je nastao i sprečiti završetak toka u [[Distribuirani sistem|distribuiranom sistemu]].

## Napomene

Zavisnost postoji između logičkih servisa, dok je konkretna komunikacija ostvarena između njihovih instanci. Odnos je usmeren: zapis `A → B` ovde znači da servis A zavisi od servisa B. Ako i B zavisi od A, postoje dve zavisnosti i nastaje ciklus.

Zavisnost može biti sinhrona ili asinhrona, jaka ili slaba i neposredna ili posredna. Te osobine određuju da li [[Otkaz komponente distribuiranog sistema|otkaz]] zavisnog servisa odmah prekida funkciju, privremeno je odlaže ili samo umanjuje njen kvalitet. Sama upotreba iste biblioteke nije zavisnost servisa, a sam redosled koraka u poslovnom toku nije dovoljan ako jedan servis za svoju funkciju ne zahteva rezultat ili ponašanje drugog.
