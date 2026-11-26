---
tip: pojam
aliases: [anti-entropy, anti-entropy process]
izvor: "Martin Kleppmann, Designing Data-Intensive Applications, O'Reilly Media, 2017, poglavlje 5, odeljak Leaderless replication, podeljak Read repair and anti-entropy; Giuseppe DeCandia i drugi, Dynamo: Amazon's Highly Available Key-value Store, SOSP '07, 2007, odeljak 4.7 Handling permanent failures: Replica synchronization, https://www.cs.purdue.edu/homes/bb/cs590/papers/amazon-dynamo-sosp2007.pdf; Apache Cassandra Documentation, Dynamo, odeljak Replica Synchronization, https://cassandra.apache.org/doc/stable/cassandra/architecture/dynamo.html; Apache Cassandra Documentation, Repair, verzija 4.0, https://svn.apache.org/repos/asf/cassandra/site/src/doc/4.0/operating/repair.html; Apache Cassandra Documentation, Tombstones, https://cassandra.apache.org/doc/latest/cassandra/managing/operating/compaction/tombstones.html"
---
# Anti-entropy

## Definicija

Anti-entropy jeste postupak koji se izvodi nezavisno od zahteva klijenata, poredi podatke [[Čvor replicirane baze|čvorova replicirane baze]] i sa jednog čvora na drugi kopira podatke koji nedostaju ili su zastareli.

## Primer

U sekundarnom kontekstu [[Cloud sistem u dve regije]], u modelu bez čvora koji određuje redosled upisa, status jednog poslovnog toka čuvaju N1, N2 i N3 ([[Leaderless replikacija]]). N3 otkaže i propusti upis tog statusa, a taj status niko ne čita, pa [[Read repair]] ne dolazi do njega. Anti-entropy poredi N3 sa N1 i N2, uočava da status nedostaje i kopira ga na N3, ali tek posle kašnjenja. Da Anti-entropy nema i da potom otkažu N1 i N2, status bi bio izgubljen, jer N3 nikada nije dobio kopiju.

## Napomene

Razlika od [[Read repair|read repair-a]]: read repair se pokreće čitanjem i popravlja samo ono što je pročitano, a Anti-entropy radi stalno i obuhvata sve podatke. Za razliku od toka izmena u replikaciji sa primarnog čvora, ne kopira upise nekim određenim redosledom, a kopiranje može da kasni.

Rad o Dynamo-u i dokumentacija Cassandra-e za poređenje podataka koriste Merkleova stabla, hash stabla u kojima se grane proveravaju nezavisno, da bi se smanjila količina podataka koja se prenosi. Rad o Dynamo-u Anti-entropy navodi kao način oporavka od trajnih otkaza. Cassandra dokumentacija navodi da read repair i hinted handoff rade koliko je moguće (best-effort), a da eventualno izjednačavanje replika obezbeđuje anti-entropy repair, i to samo ako se redovno pokreće: Cassandra ga ne pokreće sama, već operator. Rad o Dynamo-u i Kleppmann ne iznose takvu garanciju. U radu o Dynamo-u izvodi ga sam sistem u pozadini.

Anti-entropy ne može da vrati podatak koji ne postoji ni na jednoj raspoloživoj kopiji, jer samo prenosi podatke između postojećih kopija. Brisanja traže oznaku brisanja (tombstone): bez nje bi popravka vratila obrisani podatak sa čvora koji nije primio brisanje, pa oznaka mora da se čuva dovoljno dugo da stigne do svih replika. Koja je vrednost novija određuje pravilo verzionisanja sistema: Cassandra koristi last write wins, pa jedna od istovremenih izmena nestaje, a Dynamo koristi verzione vektore i čuva istovremene verzije za naknadno usklađivanje.

Knjiga navodi da nemaju svi sistemi oba mehanizma. Bez Anti-entropy-ja vrednosti koje se retko čitaju mogu ostati na manje čvorova nego što se očekuje.

Pošto u leaderless replikaciji ne postoji fiksan redosled upisa, teško je izmeriti koliko čvor zaostaje. Zato je praćenje zastarelosti podataka teže nego kod replikacije sa primarnog čvora.

U primarnom kontekstu replike R1 i R2 dobijaju izmene od [[Primarni čvor|primarnog čvora]] P ([[Replikacija podataka sa primarnog čvora na replike|replikacija]]). Čvorovi se međusobno ne porede, pa Anti-entropy nema šta da radi: P je jedini izvor izmena.

Naziv ostaje na engleskom, jer srpski prevod nije ustaljen.
