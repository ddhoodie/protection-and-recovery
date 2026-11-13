---
tip: pojam
aliases: [observability]
izvor: "Cloud Native Computing Foundation, Cloud Native Glossary, Observability, https://glossary.cncf.io/observability/"
---
# Opservabilnost (observability)

## Definicija

Opservabilnost jeste svojstvo [[Distribuirani sistem|distribuiranog sistema]] koje određuje u kojoj meri se njegovo unutrašnje stanje može razumeti na osnovu podataka koje sistem tokom rada proizvodi i čini dostupnim spolja.

## Primer

U primarnom cloud kontekstu, mehanizam za kontrolisano izazivanje otkaza uspori upise na primarnom čvoru replicirane baze, pa [[Poslovni tok kroz više servisa i baza|poslovni tok]] sporo napreduje na koraku servisa B.

[[Trag]] jednog izvršenja toka pokazuje da najveći deo trajanja tog koraka otpada na upis u bazu, ali ne dokazuje da isto važi za druga izvršenja. [[Metrika trajanja odgovora|Metrika trajanja upisa]] primarnog čvora pokazuje da je u istom periodu poraslo prosečno trajanje upisa, ali ne i zašto. [[Log|Logovi]] [[Servisna instanca|servisnih instanci]] servisa B sadrže nove zapise o obrađenim zahtevima, što pokazuje da se procesi tih instanci izvršavaju, ali ne govori ništa o instancama čiji zapisi ne stižu.

Zajedno, ovi podaci podržavaju zaključak da kašnjenje najverovatnije potiče od sporih upisa, a ne od [[Pad procesa|pada procesa]] instanci servisa B čiji zapisi stižu. Da instance beleže samo poruku da zahtev nije uspeo, sistem bi se ponašao isto, ali bi bio manje opservabilan, jer se iz takvih podataka ne bi moglo utvrditi na kom koraku nastaje kašnjenje.

## Napomene

Opservabilnost je svojstvo sistema i izražava se u meri. Praćenje (monitoring) je aktivnost prikupljanja, obrade, agregiranja i prikazivanja kvantitativnih podataka o sistemu u realnom vremenu. Sistem se može pratiti, a da njegovi podaci ipak ne omogućavaju da se razume zašto se neko ponašanje javlja.

[[Detekcija otkaza]] je odluka da se neka komponenta smatra otkazalom. Opservabilnost određuje koliko podaci o sistemu mogu da posluže kao osnova za takvu odluku, ali sama nije ta odluka.

Prisustvo logova, metrika i tragova samo po sebi ne znači da je sistem opservabilan. Presudno je da li se iz tih podataka može razumeti stanje koje je potrebno razumeti.

Izostanak podataka sam po sebi ne dokazuje da je komponenta otkazala. Isti izostanak može nastati zbog [[Pad procesa|pada procesa]], zbog [[Prekid mreže|prekida mreže]] koji sprečava prenos podataka iako se proces i dalje izvršava, zbog kašnjenja podataka ili zbog otkaza dela sistema koji ih prikuplja. Podaci dobijeni drugim putem mogu suziti moguća objašnjenja, ali veća opservabilnost ne garantuje da se ta objašnjenja uvek mogu razlikovati.
