---
tip: pojam
aliases: [conflict resolution, convergent conflict resolution]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Handling write conflicts, podeljci Converging towards a consistent state i Custom conflict resolution logic; Microsoft, Conflict types and resolution policies when using multiple write regions, Azure Cosmos DB dokumentacija, https://learn.microsoft.com/en-us/azure/cosmos-db/conflict-resolution-policies; Amazon Web Services, Using Amazon DynamoDB global tables, odeljak Overview, https://docs.aws.amazon.com/prescriptive-guidance/latest/dynamodb-global-tables/overview.html"
---
# Rešavanje sukoba (conflict resolution)

## Definicija

Rešavanje sukoba jeste postupak kojim se za podatak zahvaćen [[Sukob upisa|sukobom upisa]] određuje jedinstvena vrednost koju će imati svi [[Čvor replicirane baze|čvorovi replicirane baze]] kada prime sve izmene.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu u kome sva četiri čvora primaju upise, N1 ima status „plaćeno“ (upisan u 12:00:00), a N3 status „otkazano“ (upisan u 12:00:01). Pravilo „pobeđuje upis sa kasnijim vremenom“ (last write wins) ostavlja na oba čvora „otkazano“, pa se čvorovi slože. Upis „plaćeno“, koji je instanci servisa A već javljen kao uspešan, tiho nestaje. Ako se satovi dvaju čvorova razlikuju, može pobediti upis koji je stvarno raniji.

## Napomene

Svi čvorovi moraju da stignu do iste vrednosti, ali ta vrednost ne mora da sačuva sve upise. Knjiga navodi četiri pristupa: pobeđuje upis sa najvećim identifikatorom, na primer vremenom (last write wins), pobeđuje upis sa čvora sa većim identifikatorom, vrednosti se spoje, ili se sačuvaju sve vrednosti pa se sukob razreši kasnije. Prva dva odbacuju upise, pa i upise koji su klijentu već javljeni kao uspešni. Takav gubitak podataka nastaje i bez otkaza čvora. Dokumentacija Amazon DynamoDB global tables navodi da se sukobi razrešeni pravilom last writer wins ne beleže u CloudWatch ni CloudTrail.

Last write wins je podrazumevano pravilo u dokumentacijama Azure Cosmos DB i DynamoDB global tables. Cosmos DB dodatno nudi pravilo koje piše aplikacija. Sukobi koje to pravilo ne reši upisuju se u poseban tok sukoba (conflicts feed), pa ih aplikacija razrešava ručno. Pri last write wins u Cosmos DB obrisana verzija uvek pobeđuje umetanje i zamenu, bez obzira na vrednost.

Sukob se najjednostavnije rešava izbegavanjem: ako svi upisi jednog zapisa idu preko istog čvora, sukob ne nastaje. Zaštita prestaje kada taj čvor otkaže i saobraćaj se preusmeri na drugi, pa upisi istog zapisa ponovo mogu da stignu na različite čvorove.

Pravilo može da se izvršava pri upisu, kada baza otkrije sukob, ili pri čitanju, kada se sve vrednosti vrate aplikaciji, koja ih razrešava. Rešavanje u aplikaciji može da pogreši: knjiga navodi primer korpe za kupovinu u kojoj su se uklonjeni artikli ponovo pojavljivali.

U primarnom kontekstu, beleška [[Split-brain]] navodi tri ishoda posle ponovnog uspostavljanja veze: upisi jedne strane se odbace, spoje po unapred utvrđenom pravilu ili ručno usklade. To su tri vrste rešavanja sukoba.
