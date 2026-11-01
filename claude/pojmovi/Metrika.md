---
tip: pojam
aliases: [metric, metrics, metrike]
izvor: "Prometheus, Data model, https://prometheus.io/docs/concepts/data_model/"
---
# Metrika (metric)

## Definicija

Metrika jeste imenovana brojčana veličina koja opisuje rad ili stanje komponente [[Distribuirani sistem|distribuiranog sistema]] i čije se vrednosti beleže kroz vreme.

## Primer

U primarnom cloud kontekstu, [[Servisna instanca|servisne instance]] servisa B beleže metriku `trajanje_odgovora_ms`, a primarni čvor replicirane baze metriku `trajanje_upisa_ms`. Za svaki minut beleži se 95. percentil, odnosno vrednost koju ne prelazi 95% merenja. Kada mehanizam za kontrolisano izazivanje otkaza uspori upise, u 12:03 `trajanje_odgovora_ms` poraste sa uobičajenih 120 ms na 2.400 ms, a `trajanje_upisa_ms` sa 15 ms na 2.100 ms.

Ako je za odgovor servisa B utvrđena granica od 500 ms, prva vrednost znači da je u tom minutu najmanje 5% odgovora trajalo duže od te granice. To ukazuje na [[Usporavanje servisa|usporavanje servisa]] i potrebu za daljim ispitivanjem, ali samo po sebi ne potvrđuje otkaz ili neispravnost servisa. Druga vrednost pokazuje da su upisi na primarnom čvoru u istom periodu postali sporiji.

Istovremeni rast ukazuje na moguću vezu, ali ne potvrđuje da su spori upisi uzrok sporih odgovora. Ove metrike ne pokazuju ni zašto su upisi spori, ni koji su zahtevi bili pogođeni, niti da li su vraćeni rezultati ispravni.

## Napomene

Vrednost metrike može biti trenutna vrednost, kao što je zauzeće radne memorije u nekom trenutku, ili sažetak merenja iz određenog perioda, kao što je 95. percentil trajanja odgovora za jedan minut.

Metrika pokazuje kako se neka veličina menja kroz vreme, [[Log|log]] šta se dogodilo u pojedinačnim događajima, a [[Trag|trag]] kuda je prošao jedan zahtev. Metrika zato brzo otkriva promenu u ponašanju, ali kada sažima merenja, gubi pojedinačne zahteve koje druga dva izvora mogu da prikažu.

Izbor metrika i načina sažimanja utiče na [[Opservabilnost|opservabilnost]] sistema. Prosek može da prikrije mali deo veoma sporih zahteva koji se vidi u visokom percentilu. Posle uklanjanja jedine spore instance iz saobraćaja metrika trajanja odgovora može da se vrati na uobičajenu vrednost, iako je kapacitet servisa smanjen, jer meri samo zahteve koje obrađuju preostale instance.

Metrika se razlikuje od mera oporavka kao što je [[Procenat uspešnih zahteva tokom otkaza|procenat uspešnih zahteva tokom otkaza]]. Takva mera se određuje za unapred utvrđen interval i kriterijum uspeha, a metrike mogu da budu podaci iz kojih se računa.
