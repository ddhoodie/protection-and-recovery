---
tip: pojam
aliases: ["response time metric", "latency metric", "metrika latencije"]
izvor: "Betsy Beyer, Chris Jones, Jennifer Petoff i Niall Richard Murphy, Site Reliability Engineering, poglavlje 6 Monitoring Distributed Systems, odeljci The Four Golden Signals i Worrying About Your Tail, https://sre.google/sre-book/monitoring-distributed-systems/"
---
# Metrika trajanja odgovora (response time metric)

## Definicija

Metrika trajanja odgovora jeste imenovana brojčana veličina koja opisuje koliko vremena komponenta [[Distribuirani sistem|distribuiranog sistema]] troši da odgovori na zahteve i čije se vrednosti beleže kroz vreme, obično kao sažetak merenja iz određenog perioda.

## Primer

U primarnom cloud kontekstu, [[Servisna instanca|servisne instance]] servisa B beleže metriku trajanja odgovora `trajanje_odgovora_ms`, a primarni čvor replicirane baze metriku `trajanje_upisa_ms`. Za svaki minut beleži se 95. percentil, odnosno vrednost koju ne prelazi 95% merenja. Kada mehanizam za kontrolisano izazivanje otkaza uspori upise, u 12:03 `trajanje_odgovora_ms` poraste sa uobičajenih 120 ms na 2.400 ms, a `trajanje_upisa_ms` sa 15 ms na 2.100 ms.

Ako je za odgovor servisa B utvrđena granica od 500 ms, prva vrednost znači da je u tom minutu najmanje 5% odgovora trajalo duže od te granice. To ukazuje na [[Usporavanje servisa|usporavanje servisa]] i potrebu za daljim ispitivanjem, ali samo po sebi ne potvrđuje otkaz ili neispravnost servisa. Druga vrednost pokazuje da su upisi na primarnom čvoru u istom periodu postali sporiji.

Istovremeni rast ukazuje na moguću vezu, ali ne potvrđuje da su spori upisi uzrok sporih odgovora. Ove metrike ne pokazuju ni zašto su upisi spori, ni koji su zahtevi bili pogođeni, niti da li su vraćeni rezultati ispravni.

## Napomene

Metrika trajanja odgovora je jedna vrsta metrike. Celina je izdvaja jer najčešće prva pokazuje da je odgovor spor, a spor odgovor ne mora značiti pad komponente. Ostale metrike, kao što su zauzeće procesora ili broj zahteva u sekundi, ovde se ne obrađuju posebno.

Način sažimanja utiče na [[Opservabilnost|opservabilnost]] sistema. Prosek može da prikrije mali deo veoma sporih zahteva, dok se oni vide u visokom percentilu. Zato se trajanje odgovora obično sažima kao percentil za kratak period, na primer za jedan minut.

Trajanje neuspešnih zahteva prati se odvojeno od trajanja uspešnih. Ako primarni čvor ne prihvata upise, a servis B odmah vraća grešku, trajanje odgovora može da se smanji iako servis ne obavlja svoj rad.

Posle uklanjanja jedine spore instance iz saobraćaja metrika trajanja odgovora može da se vrati na uobičajenu vrednost, iako je kapacitet servisa smanjen, jer meri samo zahteve koje obrađuju preostale instance.

Metrika trajanja odgovora pokazuje kako se trajanje menja kroz vreme, [[Log|log]] šta se dogodilo u pojedinačnim događajima, a [[Trag|trag]] gde je vreme potrošeno u jednom zahtevu. Metrika zato brzo otkriva promenu u ponašanju, ali kada sažima merenja, gubi pojedinačne zahteve koje druga dva izvora mogu da prikažu.

Metrika trajanja odgovora samo meri. [[Rok čekanja]] određuje kada onaj ko čeka prestaje da čeka, a vremenska granica iz beleške [[Usporavanje servisa]] kada se odgovor smatra sporim. Od mera oporavka, kao što je [[Procenat uspešnih zahteva tokom otkaza|procenat uspešnih zahteva tokom otkaza]], razlikuje se po tome što se beleži stalno, dok se mera oporavka određuje za unapred utvrđen interval i kriterijum uspeha. Metrike mogu da budu podaci iz kojih se takva mera računa.
