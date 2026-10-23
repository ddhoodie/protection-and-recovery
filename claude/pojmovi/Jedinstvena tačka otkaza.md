---
tip: pojam
aliases: [SPOF, single point of failure]
izvor: "AWS Prescriptive Guidance, Resilience analysis framework - Overview of the framework, https://docs.aws.amazon.com/prescriptive-guidance/latest/resilience-analysis-framework/overview.html"
---
# Jedinstvena tačka otkaza (single point of failure, SPOF)

## Definicija

Jedinstvena tačka otkaza jeste element [[Distribuirani sistem|distribuiranog sistema]] čiji je pojedinačni [[Otkaz komponente distribuiranog sistema|otkaz]] dovoljan da prekine određenu zahtevanu funkciju sistema zato što ne postoji operativno nezavisna alternativa koja može da preuzme njegovu ulogu u granicama ispravnosti te funkcije.

## Primer

U primarnom cloud kontekstu, više [[Servisna instanca|servisnih instanci]] radi iza jednog balansera. Ako ne postoji drugi pristupni put do instanci, taj balanser je jedinstvena tačka otkaza: njegov otkaz prekida pristup funkcijama sistema iako su servisne instance i baza ispravne. Više instanci zato ne uklanja ovu jedinstvenu tačku otkaza, jer sve zavise od istog balansera.

## Napomene

Jedinstvena tačka otkaza je svojstvo arhitekture i njenih zavisnosti, a ne naziv za sam događaj otkaza. Element može biti SPOF za jednu funkciju, a da druge funkcije ne zavise od njega. Ako njegov otkaz onemogući sve zahtevane funkcije na granici sistema, posledica je [[Potpuni otkaz sistema]].

Samo postojanje više zamenskih elemenata nije dovoljno. Alternative moraju biti sposobne da preuzmu istu ulogu u zahtevanim granicama i ne smeju sve zavisiti od istog elementa čijim bi otkazom zajedno postale neupotrebljive. [[Graf zavisnosti]] može pomoći u pronalaženju elemenata kroz koje prolaze sve zavisnosti potrebne za određenu funkciju.
