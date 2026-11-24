---
tip: pojam
aliases: [leader lease, lease]
izvor: "Cary G. Gray i David R. Cheriton, Leases: An Efficient Fault-Tolerant Mechanism for Distributed File Cache Consistency, Proceedings of the 12th ACM Symposium on Operating Systems Principles (SOSP), 1989, str. 202-210"
---
# Zakup uloge primarnog čvora (leader lease)

## Definicija

Zakup uloge primarnog čvora jeste vremenski ograničeno pravo čvora baze podataka da ima ulogu [[Primarni čvor|primarnog čvora]], koje mu dodeljuje [[Kvorum|kvorum]] i koje čvor mora da obnovi pre isteka, a po čijem isteku bez obnove sam prestaje da prihvata upise.

## Primer

U primarnom cloud kontekstu, primarni čvor P ima zakup od 10 sekundi i obnavlja ga svake 2 sekunde potvrdama od R1 i R2. U 12:00:00 [[Mrežna particija|mrežna particija]] odvoji zonu 1, u kojoj je P. Poslednja obnova je bila u 11:59:58, pa zakup ističe u 12:00:08. Do tada P prihvata upise servisnih instanci iz zone 1, a od 12:00:08 ih odbija, iako se proces baze i dalje izvršava i niko spolja nije zaustavio čvor. Na drugoj strani R1 i R2 čekaju da istekne najduži zakup koji je P mogao da ima, pa tek posle toga R1 postaje primarni čvor. U svakom trenutku najviše jedan čvor prihvata upise.

## Napomene

Zakup se razlikuje od [[Fencing|fencing-a]] po tome ko zaustavlja stari primarni čvor. Kod zakupa čvor prestaje sam, na osnovu sopstvenog sata i bez ikakve poruke. Kod fencing-a ga zaustavlja druga komponenta, bez oslanjanja na njegovu saradnju. Mehanizmi se dopunjuju, a ne isključuju.

Zakup je bezbedan samo ako satovi čvorova ne odstupaju više od unapred pretpostavljene granice i ako proces ne stane na duže vreme. Ako proces čvora P zastane 15 sekundi, na primer zbog čišćenja memorije, posle nastavka može da prihvati upis verujući da mu zakup još važi. Zato se uz zakup koristi i provera tokena kod fencing-a.

Novi primarni čvor ne sme da počne da prihvata upise pre nego što istekne zakup starog. Čekanje na istek zakupa ulazi u ostvareno trajanje oporavka, pa duži zakup smanjuje broj obnova, ali produžava vreme bez primarnog čvora u odnosu na [[Ciljno vreme oporavka|RTO]].
