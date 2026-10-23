---
tip: pojam
aliases: [number of workflows in an inconsistent state, inconsistent workflow count]
izvor: "Microsoft Azure Architecture Center, Saga distributed transactions pattern, https://learn.microsoft.com/en-us/azure/architecture/patterns/saga"
---
# Broj tokova u nekonzistentnom stanju (number of workflows in an inconsistent state)

## Definicija

Broj tokova u nekonzistentnom stanju jeste broj jedinstvenih izvršenja [[Poslovni tok kroz više servisa i baza|poslovnog toka kroz više servisa i baza]] u određenom obimu i trenutku čije sačuvano stanje preko uključenih servisa i baza krši najmanje jedno unapred utvrđeno pravilo usklađenosti tog toka.

## Primer

U primarnom cloud kontekstu, kontrolisani otkaz prekine 100 izvršenja poslovnog toka. Posle oporavka, sedam izvršenja ima zabeležen završen korak u bazi servisa A, dok odgovarajući obavezni korak u bazi servisa B nije ni završen ni poništen. Ako pravilo toka ne dozvoljava tu kombinaciju stanja, broj tokova u nekonzistentnom stanju iznosi sedam. Svako izvršenje broji se jednom, čak i kada krši više pravila.

## Napomene

Pravila usklađenosti i trenutak merenja moraju biti određeni pre eksperimenta. Delimično izvršen tok nije nužno nekonzistentan ako je njegovo trenutno stanje dozvoljeno i sistem predviđa njegov dalji napredak ili poništavanje.

Mera ne pokazuje ozbiljnost, trajanje ni uzrok svake nekonzistentnosti. Takođe zahteva stabilan identitet izvršenja kako isti tok ne bi bio prebrojan više puta kroz zapise različitih servisa.
