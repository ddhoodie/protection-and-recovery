---
tip: pojam
aliases: [timeout, time-out]
izvor: "gRPC Documentation, Deadlines, odeljci Overview, Deadlines on the Server i Deadline Propagation, https://grpc.io/docs/guides/deadlines/"
---
# Rok čekanja (timeout)

## Definicija

Rok čekanja jeste unapred određeno najduže trajanje tokom kojeg komponenta [[Distribuirani sistem|distribuiranog sistema]] čeka odgovor ili drugi očekivani događaj, a po čijem isteku prestaje da čeka i to čekanje smatra neuspešnim.

## Primer

U primarnom cloud kontekstu, servis A ima [[Zavisnost servisa|zavisnost]] od servisa B. Ako je za taj poziv određen rok od 1.000 ms, a mehanizam za kontrolisano izazivanje otkaza uspori upise na primarnom čvoru replicirane baze tako da obrada zahteva u servisu B traje 2.400 ms, servis A posle 1.000 ms prestaje da čeka i poziv smatra neuspešnim.

Ako rok nije prenet servisu B, njegova [[Servisna instanca|servisna instanca]] za to vreme može da nastavi obradu i završi upis, pa servis A ne zna da li je izmena izvršena. Ovde je uzrok [[Usporavanje servisa|usporavanje servisa]], ali bi isti istek roka nastao i posle [[Pad procesa|pada procesa]] ili [[Prekid mreže|prekida mreže]], pa sam istek ne pokazuje koji se slučaj dogodio.

## Napomene

Istek roka opisuje ishod čekanja kod onoga ko čeka, a ne ishod operacije kod onoga ko je obrađuje. Zato ponavljanje iste operacije posle isteka roka može da izazove da se ona izvrši dva puta.

Prekratak rok proglašava neuspešnim operacije koje bi se uspešno završile. Predug rok odlaže reakciju i duže zadržava resurse, kao što su niti i veze, dok traje čekanje.

U lancu poziva, na primer servis A → servis B → primarni čvor replicirane baze, rok čekanja može da se prenese niz [[Zavisnost servisa|zavisnosti]], tako da svaki sledeći poziv dobija samo preostali deo roka. Ako se rok ne prenosi, servis B nastavlja obradu i pošto je servis A odustao, pa opterećuje sporu bazu poslom čiji rezultat niko ne čeka. Prenet rok sam po sebi ne zaustavlja obradu, već servis B mora da prekine započeti rad kada rok istekne.

Rok čekanja određuje kada onaj ko čeka odustaje, dok vremenska granica iz beleške [[Usporavanje servisa]] određuje kada se odgovor smatra sporim. Te dve vrednosti ne moraju biti iste. Granica bez napretka iz beleške [[Broj tokova u zaglavljenom stanju]] odnosi se na izvršenje toka, a ne na pojedinačno čekanje.

Rok čekanja koriste i [[Provera zdravlja servisne instance|provera zdravlja]] i prijem [[Signal života|signala života]]. Njegov istek je opažanje, a ne [[Detekcija otkaza|detekcija otkaza]].
