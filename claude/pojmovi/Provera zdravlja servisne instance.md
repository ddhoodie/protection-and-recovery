---
tip: pojam
aliases: [health check, service instance health check, provera zdravlja]
izvor: "Microsoft Azure Architecture Center, Health Endpoint Monitoring pattern, odeljak Solution, https://learn.microsoft.com/en-us/azure/architecture/patterns/health-endpoint-monitoring"
---
# Provera zdravlja servisne instance (health check)

## Definicija

Provera zdravlja servisne instance jeste periodični test [[Servisna instanca|servisne instance]] čiji se ishod ocenjuje prema unapred određenom kriterijumu uspeha, kako bi se procenilo da li je instanca sposobna da obavlja svoj rad.

## Primer

U primarnom cloud kontekstu, balanser opterećenja svakih 10 s šalje zahtev `GET /health` svakoj instanci servisa B. Provera je uspešna ako instanca u [[Rok čekanja|roku od 2 s]] vrati HTTP 200. Balanser zatim može da zabeleži dva uzastopna neuspeha, a to je samo opažanje.

Kada jedna instanca prestane da odgovara, provera ne uspeva, ali sam neuspeh ne pokazuje da li je nastao [[Pad procesa|pad procesa]], [[Prekid mreže|prekid mreže]] između balansera i instance ili je instanca samo spora. Ograničen je i uspeh. Ako `/health` ne koristi bazu, a mehanizam za kontrolisano izazivanje otkaza uspori upise na primarnom čvoru replicirane baze, instance i dalje prolaze proveru iako [[Poslovni tok kroz više servisa i baza|poslovni tok]] sporo napreduje.

## Napomene

Provera može da potvrdi samo ono što ispituje. Plitka provera utvrđuje da li instanca može da odgovori, dok duboka ispituje i ono od čega njen rad zavisi. Plitka provera zato može da prođe iako instanca ne može da obavi svoju funkciju, kao što opisuje beleška [[Zavisnost servisa]].

Duboka provera nosi suprotan rizik. Ako otkaže zavisnost koju koriste sve instance, sve one mogu istovremeno da ne prođu proveru, iako ih uklanjanje iz saobraćaja ili ponovno pokretanje neće popraviti. Mehanizam provere tada može da doprinese [[Širenje otkaza kroz graf zavisnosti|širenju otkaza]]. Zato se provera da li proces radi i provera da li instanca može da obavi svoj rad često izvode odvojeno.

Metrike, [[Log|logovi]] i [[Trag|tragovi]] nastaju tokom redovnog rada sistema, dok se provera zdravlja izvršava namenski, radi ispitivanja instance. Njen ishod je još jedan izvor podataka koji doprinosi [[Opservabilnost|opservabilnosti]].

Neuspela provera nije isto što i [[Detekcija otkaza|detekcija otkaza]]. Ona je opažanje na osnovu kojeg se, često tek posle više uzastopnih neuspeha, donosi odluka o stanju instance.
