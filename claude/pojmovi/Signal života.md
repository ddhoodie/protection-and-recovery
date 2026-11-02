---
tip: pojam
aliases: [heartbeat, heartbeat message, heartbeat poruka]
izvor: "Unmesh Joshi, Patterns of Distributed Systems, HeartBeat, odeljci Problem i Solution, https://martinfowler.com/articles/patterns-of-distributed-systems/heartbeat.html"
---
# Signal života (heartbeat)

## Definicija

Signal života jeste poruka koju komponenta [[Distribuirani sistem|distribuiranog sistema]] periodično i bez prethodnog zahteva šalje drugim komponentama da bi pokazala da se i dalje izvršava.

## Primer

U primarnom cloud kontekstu, primarni čvor replicirane baze svakih 100 ms šalje signal života replikama. Replika koja primi poruku može da zaključi da se primarni čvor izvršavao u trenutku slanja, ali ne i da se izvršava sada.

Ako replika ne primi nijednu poruku tokom 1 s, ona ne može samo na osnovu toga da utvrdi da li je nastao [[Pad procesa|pad procesa]] primarnog čvora, [[Prekid mreže|prekid mreže]] između njih ili je primarni čvor toliko opterećen da poruke kasne. Ni prijem poruka nema širi značaj. Ako mehanizam za kontrolisano izazivanje otkaza uspori upise, primarni čvor i dalje može redovno da šalje signal života iako su upisi spori.

## Napomene

Signal života šalje sama komponenta, dok [[Provera zdravlja servisne instance|proveru zdravlja]] pokreće neko drugi, koji i ocenjuje njen ishod. Zato izostanak signala života govori samo da poruka nije stigla, a sadržaj provere može da se prilagodi onome što treba ispitati.

Signal života pokazuje da se komponenta izvršava, a ne da ispravno obavlja svoju funkciju. Za razliku od [[Log|loga]] i [[Metrika|metrike]], on sam po sebi ne opisuje šta se u komponenti dešava, pa je njegov doprinos [[Opservabilnost|opservabilnosti]] ograničen.

Izostanak signala života je opažanje, a ne [[Detekcija otkaza|detekcija otkaza]]. Kraći [[Rok čekanja|rok čekanja]] omogućava brže reagovanje, ali češće proglašava spore komponente neispravnim, a duži rok odlaže otkrivanje stvarnog otkaza.
