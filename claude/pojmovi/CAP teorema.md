---
tip: pojam
aliases: [CAP theorem, Brewer's theorem]
izvor: "Seth Gilbert i Nancy Lynch, Brewer's Conjecture and the Feasibility of Consistent, Available, Partition-Tolerant Web Services, ACM SIGACT News, 33(2), 2002, str. 51-59"
---
# CAP teorema (CAP theorem)

## Definicija

CAP teorema jeste tvrđenje da [[Replicirana baza u cloud-u|replicirana baza]] ne može tokom [[Mrežna particija|mrežne particije]] istovremeno da obezbedi jaku [[Konzistentnost podataka|konzistentnost podataka]] i dostupnost. Dostupnost ovde znači da svaki čvor koji radi na svaki zahtev pre ili kasnije vrati odgovor koji nije greška.

## Primer

U primarnom cloud kontekstu, mrežna particija podeli sistem u dve grupe. U prvoj grupi su [[Primarni čvor|primarni čvor]] i deo servisnih instanci, koje i dalje upisuju nove izmene. U drugoj grupi su [[Replika|replike]] i servis B, koji traži status poslovnog toka. Replika ne može da zna da li je primarni čvor u međuvremenu potvrdio novu izmenu tog toka. Ona može da odbije čitanje i vrati grešku, čime se čuva konzistentnost, ali servis B ne dobija podatak i gubi se dostupnost. Ili može da vrati podatak koji ima, pa servis B dobija odgovor, ali on može biti zastareo. Treća mogućnost, da replika vrati podatak za koji je sigurno da je najnoviji, ne postoji dok particija traje.

## Napomene

Teorema se često prepričava kao „od tri svojstva biraju se dva“, ali to je netačno. Mrežna particija nije svojstvo koje se bira, nego događaj koji sistem ne može da spreči. Izbor između konzistentnosti i dostupnosti postoji samo dok particija traje. Dok je mreža ispravna, sistem može da pruža oba svojstva.

Teorema važi za svaki [[Distribuirani sistem|distribuirani sistem]] koji čuva kopije istih podataka na više čvorova, a ne samo za repliciranu bazu sa primarnim čvorom. 

Dostupnost u ovoj teoremi ne znači da čvor odgovara brzo, niti da ceo sistem radi.

Konzistentnost u teoremi jeste jaka konzistentnost (linearizabilnost), najviši nivo konzistentnosti podataka. Za slabije nivoe, kao što je konačna konzistentnost, teorema ne tvrdi ništa.

Kako se izbor pravi u konkretnom sistemu opisuje [[Kompromis konzistentnosti i dostupnosti tokom mrežne particije]].
