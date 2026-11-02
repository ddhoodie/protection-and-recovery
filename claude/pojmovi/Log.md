---
tip: pojam
aliases: [logs, logovi]
izvor: "OpenTelemetry Specification, Glossary, odeljci Log Record i Log, https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/glossary.md"
---
# Log (log)

## Definicija

Log jeste skup vremenski označenih zapisa koje komponenta [[Distribuirani sistem|distribuiranog sistema]] proizvodi tokom rada, pri čemu svaki zapis opisuje jedan događaj u tom radu.

## Primer

U primarnom cloud kontekstu, svaka [[Servisna instanca|servisna instanca]] servisa B proizvodi sopstveni log. Kada mehanizam za kontrolisano izazivanje otkaza uspori upise na primarnom čvoru replicirane baze, log jedne instance dobije zapis `12:03:41 INFO obrada zahteva završena, upis u bazu trajao 2,1 s`.

Taj zapis pokazuje da je instanca u 12:03:41 završila obradu tog zahteva i koliko je, po njenom merenju, trajao upis. On ne pokazuje koliko je takvih sporih upisa bilo u celom servisu, niti zašto je upis bio spor. Ako novi zapisi prestanu da stižu, to samo po sebi ne dokazuje [[Pad procesa|pad procesa]], jer [[Prekid mreže|prekid mreže]] može da spreči prenos zapisa iako se proces i dalje izvršava.

## Napomene

Reč log se u praksi koristi i za ceo skup zapisa i za pojedinačan zapis. U ovoj bazi log označava skup, a pojedinačan element tog skupa je zapis loga.

Log doprinosi [[Opservabilnost|opservabilnosti]] sistema samo ako su njegovi zapisi dostupni spolja i ako sadrže podatke iz kojih se može razumeti potrebno stanje. Samo postojanje loga to ne garantuje.

[[Metrika]] beleži brojčane vrednosti kroz vreme, trenutne ili sažete za neki period, dok log čuva pojedinačne događaje. [[Trag]] prati put jednog zahteva kroz više servisa, dok zapis loga ne mora da pripada nijednom određenom zahtevu.

Dnevnik transakcija baze podataka (transaction log, write-ahead log) razlikuje se od logova opisanih u ovoj belešci. On beleži izmene podataka, a sistemi kao što su PostgreSQL i SQL Server koriste ga za oporavak baze i za prenos izmena na replike.
