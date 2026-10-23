---
tip: pojam
aliases: [service instance]
izvor: "OASIS S-RAMP Version 1.0, Part 1: Foundation, odeljak 2.3.2.1, https://docs.oasis-open.org/s-ramp/s-ramp/v1.0/s-ramp-v1.0-part1-foundation.html"
---
# Servisna instanca (service instance)

## Definicija

Servisna instanca jeste konkretno pokrenuto izvršenje implementacije aplikativnog servisa, sa zasebnim identitetom i stanjem izvršavanja, koje se može pokrenuti, zaustaviti ili zameniti nezavisno od drugih instanci istog servisa.

## Primer

Iza balansera istovremeno radi više instanci istog aplikativnog servisa. Kada jedna instanca otkaže, prestaje da obrađuje zahteve, dok druge instance istog servisa mogu nastaviti rad. Pokrenuta zamena predstavlja novu servisnu instancu, čak i kada koristi isti programski kod i konfiguraciju kao instanca koja je otkazala.

## Napomene

Servis je logička funkcionalnost i ugovor koji pruža, dok je servisna instanca njegovo konkretno izvršenje. Proces, kontejner, pod ili virtuelna mašina nisu univerzalni sinonimi za servisnu instancu. Endpoint je mesto preko kojeg se instanci pristupa, a ne sama instanca.

