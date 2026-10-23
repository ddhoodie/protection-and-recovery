---
tip: pojam
aliases: ["cross-service, multi-database workflow", cross-service workflow, međuzavisni tok, interdependent workflow, višeservisni poslovni tok]
izvor: "OASIS Web Services Business Process Execution Language Version 2.0, OASIS Standard, odeljak 1, https://docs.oasis-open.org/wsbpel/2.0/OS/wsbpel-v2.0-OS.pdf"
---
# Poslovni tok kroz više servisa i baza (cross-service, multi-database workflow)

## Definicija

Poslovni tok kroz više servisa i baza jeste niz ili mreža međusobno uslovljenih koraka kojima [[Aplikativni sistem|aplikativni sistem]] ostvaruje poslovni cilj, pri čemu korake izvršava više aplikativnih servisa, a koraci pristupaju podacima u više baza.

## Primer

U poslovnom toku primarnog cloud sistema, servis A u svojoj bazi beleži rezultat prvog koraka, servis B koristi taj rezultat i menja podatke u drugoj bazi, a servis C završava tok tek kada dobije potvrdu o prethodnom koraku. Ako servis B otkaže nakon što je prvi korak trajno završen, tok ostaje delimično izvršen: pojedine [[Servisna instanca|servisne instance]] mogu biti zdrave, ali poslovni cilj nije ostvaren i podaci toka nisu u usklađenom završnom stanju. Oporavak zato mora da utvrdi koji su koraci uspeli i da preostali rad nastavi, ponovi ili poništi.

## Napomene

Termin nema potpuno ustaljen engleski ekvivalent. Izraz *cross-service workflow* ističe učešće više servisa, ali ne iskazuje da su podaci raspoređeni u više baza. Prošireni izraz *cross-service, multi-database workflow* preciznije odgovara značenju iz ove baze. Raniji naziv „međuzavisni tok“ ostaje alias, ali je manje precizan jer može označavati i više zasebnih tokova koji zavise jedan od drugog.

[[Graf zavisnosti]] pokazuje koji servisi zavise jedan od drugog, dok poslovni tok opisuje konkretne korake, njihov redosled i promene stanja koje vode ka poslovnom cilju. Dva servisa mogu biti povezana u grafu zavisnosti, a da ne učestvuju u svakom izvršenju istog toka. Definicija toka opisuje moguće korake i njihove veze, dok svako izvršenje toka ima sopstveni napredak i stanje.
