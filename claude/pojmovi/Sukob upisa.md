---
tip: pojam
aliases: [write conflict]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljci Handling write conflicts i Failover; PostgreSQL Documentation, odeljak 13.2 Transaction Isolation, https://www.postgresql.org/docs/current/transaction-iso.html; Microsoft, Conflict types and resolution policies when using multiple write regions, Azure Cosmos DB dokumentacija, https://learn.microsoft.com/en-us/azure/cosmos-db/conflict-resolution-policies"
---
# Sukob upisa (write conflict)

## Definicija

Sukob upisa jeste stanje u kome su dva [[Istovremenost upisa|istovremena upisa]] izmenila isti podatak na različitim [[Čvor replicirane baze|čvorovima replicirane baze]], pa se samo na osnovu tih upisa ne može odrediti jedinstvena vrednost podatka.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu u kome sva četiri čvora primaju upise, za vreme prekida mreže između regija instanca servisa A upisuje na N1 status „plaćeno“, a instanca servisa B upisuje na N3 status „otkazano“. Obema instancama je upis javljen kao uspešan. Kada prekid prestane, N1 primi „otkazano“, a N3 primi „plaćeno“. Ako bi svaki čvor jednostavno primenio izmenu onim redom kojim je stiže, N1 bi završio sa „otkazano“, a N3 sa „plaćeno“, pa bi se čvorovi trajno razilazili. Sukob se otkriva tek sada, kada je obema instancama upis već potvrđen.

## Napomene

Dok upise istog podatka prima samo jedan primarni čvor, on određuje njihov redosled, pa sukob upisa u smislu ove definicije ne nastaje: drugi upis ili čeka prvi, ili se prekida, ili se, zavisno od nivoa izolacije, izvršava nad već izmenjenom vrednošću. Time se ne isključuju sve konkurentne izmene na aplikativnom nivou (vidi poslednji pasus). Pretpostavka o jednom primarnom čvoru ne važi kada se poremeti njegova uloga: posle [[Failover|failover-a]] novi primarni čvor može imati upise koji se sukobljavaju sa upisima koje stari nije stigao da prenese, a u slučaju [[Split-brain|split-brain-a]] i u modelu koji ga ne predviđa. U [[Multi-leader replikacija|multi-leader]] i [[Leaderless replikacija|leaderless]] replikaciji sukob je redovan. U primarnom kontekstu to je situacija iz primera beleške Split-brain: izmene istog zapisa poslovnog toka na čvoru P i na čvoru R1.

Razlika od [[Split-brain|split-brain-a]]: split-brain je stanje u kome su čvorovi nezavisno prihvatali upise kao primarni, a sukob upisa je posledica na nivou podatka. U multi-leader replikaciji sukob je očekivan i za njega mora postojati pravilo, dok je u split-brain-u neočekivan. Nerazrešen sukob vodi razilaženju podataka, a to može ostaviti poslovne tokove u nekonzistentnom stanju.

Izmena obuhvata umetanje, zamenu i brisanje. Dokumentacija Azure Cosmos DB razlikuje tri oblika sukoba pri upisu u više regija: istovremeno umetanje stavki sa istim jedinstvenim ključem, istovremenu zamenu iste stavke i brisanje u jednoj regiji uz istovremenu izmenu u drugoj.

Definicija obuhvata samo upise istog podatka. Knjiga navodi i suptilniji slučaj: pravilo nad više podataka, na primer da se ista prostorija ne sme rezervisati dva puta u isto vreme, može biti prekršeno upisima na različitim čvorovima, iako nijedan podatak nije dvaput izmenjen. Taj slučaj ovde nije obuhvaćen. Na jednom čvoru ta pravila čuvaju ograničenja i nivo izolacije transakcija.
