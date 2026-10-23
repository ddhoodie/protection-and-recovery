---
tip: pojam
aliases: [number of workflows in a stuck state, stuck workflow count]
izvor: "AWS Step Functions Developer Guide, Using timeouts to avoid stuck Step Functions workflow executions, https://docs.aws.amazon.com/step-functions/latest/dg/sfn-best-practices.html#bp-timeouts"
---
# Broj tokova u zaglavljenom stanju (number of workflows in a stuck state)

## Definicija

Broj tokova u zaglavljenom stanju jeste broj jedinstvenih nezavršenih izvršenja [[Poslovni tok kroz više servisa i baza|poslovnog toka kroz više servisa i baza]] koja u trenutku posmatranja nisu ostvarila očekivani napredak duže od unapred određene vremenske granice iako njihov poslovni cilj još nije ni ostvaren ni konačno napušten.

## Primer

Posle kontrolisanog otkaza u primarnom cloud kontekstu, četiri izvršenja poslovnog toka ostanu u koraku koji čeka odgovor servisa B. Za taj korak je kao granica bez napretka utvrđeno pet minuta. Ako ni posle pet minuta nema odgovora, ponovnog pokušaja, prelaska na sledeći korak, poništavanja ni konačnog neuspeha, broj tokova u zaglavljenom stanju iznosi četiri.

## Napomene

Granica bez napretka mora da odgovara očekivanom trajanju konkretnog koraka ili toka. Prekratka granica pogrešno označava spora ali ispravna izvršenja, dok preduga odlaže otkrivanje stvarno zaglavljenih tokova.

Zaglavljen tok može imati međusobno usklađene podatke, ali ne napreduje. Nasuprot tome, tok obuhvaćen merom [[Broj tokova u nekonzistentnom stanju|broja tokova u nekonzistentnom stanju]] može i dalje aktivno da se oporavlja. Zato se te dve mere ne zamenjuju.
