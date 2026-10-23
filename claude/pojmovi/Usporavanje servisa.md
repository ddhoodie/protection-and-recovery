---
tip: pojam
aliases: [service slowdown, excessive service latency, service performance degradation]
izvor: "AWS Prescriptive Guidance, Resilience analysis framework - Overview of the framework, https://docs.aws.amazon.com/prescriptive-guidance/latest/resilience-analysis-framework/overview.html"
---
# Usporavanje servisa (service slowdown)

## Definicija

Usporavanje servisa jeste stanje u kojem funkcija koju pružaju njegove [[Servisna instanca|servisne instance]] ostaje dostupna i daje ispravan rezultat, ali obrada ili odgovor traju duže od utvrđene ili očekivane vremenske granice za tu funkciju.

## Primer

U primarnom cloud kontekstu, instance servisa B i dalje obrađuju zahteve i vraćaju ispravne rezultate, ali kontrolisano opterećenje produži vreme odgovora sa uobičajenih 100 ms na nekoliko sekundi. Servis A, koji ima [[Zavisnost servisa|zavisnost]] od rezultata servisa B, zato ne može da završi svoj korak poslovnog toka u zahtevanom vremenu. Procesi servisa B nisu pali, ali je servis usporen.

## Napomene

Usporavanje je određeno u odnosu na vremensku granicu koja može poticati iz specifikacije, cilja nivoa usluge ili očekivanja pozivaoca. Sam porast vremena odziva nije nužno usporavanje u ovom smislu ako rezultat i dalje stiže unutar relevantne granice.

Usporavanje se razlikuje od [[Pad procesa|pada procesa]] jer proces može nastaviti da izvršava korake i proizvodi ispravne rezultate. Ako odgovor kasni izvan granica ispravnosti funkcije, usporavanje istovremeno predstavlja [[Otkaz komponente distribuiranog sistema|otkaz]] po vremenu odziva.

Jedna spora servisna instanca ne mora da uspori servis ako je balanser ukloni iz saobraćaja ili druge instance održe zahtevano vreme odziva. Zato se stanje pojedinačne instance i ponašanje funkcije servisa mere odvojeno.
