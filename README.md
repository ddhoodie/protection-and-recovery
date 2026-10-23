# Tim 2 · Zaštita i oporavak

Ovo je repozitorijum baze znanja tima 2. Baza je skup pojmova sa definicijama i primerima, u markdownu, za temu oporavka distribuiranih sistema u cloud-u. Nije folder za slajdove i nije zapis časa.

Baza se gradi skillom u `claude/SKILL.md`. Skill čita konfiguraciju, razgovara o pojmu i upisuje belešku. Na času se ti pojmovi izlažu. Na git ide baza. Prezentacija ostaje kod onoga ko je drži.

Kvalitet baze meri se time koliko precizno njeni pojmovi omogućavaju da se opiše problem iz konfiguracije i projektuje rešenje.

## Mapa

```
README.md                 ovo uputstvo
uloge_tim2.xlsx           ko je koja uloga na kom času
claude/
  SKILL.md                uputstvo za model koji vodi izgradnju baze
  assets/                 prazni šabloni, nisu baza
  _meta/                  konfiguracija i odluke, važe za celu bazu
  konteksti/              sistemi u kojima žive primeri
  pojmovi/                jedna beleška po pojmu
```

## Čemu služi koji folder

### `claude/pojmovi/`

Ovde je sadržaj koji se predaje i review-uje. Jedan fajl je jedan pojam. Ime fajla je srpski termin u nominativu jednine, na primer `Ciljno vreme oporavka.md`.

Beleška ima definiciju, primer u primarnom kontekstu i izvor. Definicija sme da koristi samo pojmove koji već imaju belešku ili su u `_meta/odluke.md` označeni kao pretpostavljeni. Veze su Obsidian linkovi, npr. `[[Ciljno vreme oporavka|ciljnog vremena oporavka]]`.


### `claude/konteksti/`

Zajednička scena za primere, da se pojmovi ne objašnjavaju na nepovezanim pričama.


### `claude/_meta/`

Podaci o celoj bazi, ne o jednom pojmu. Skill ovo čita pre bilo kakvog rada. Dva fajla:

`konfiguracija.md` kaže šta je tema, koji problem se rešava, ko je publika i šta publika već zna, na kom jeziku se piše i koji kontekst je primarni. Za ovu bazu tema je oporavak distribuiranih sistema u cloud-u posle otkaza baza, servisnih instanci i poslovnih tokova. Konfiguracija je popunjena. Novi prolazak kroz skill je ne pravi ponovo i ne prepisuje je za svaki pojam.

`odluke.md` pamti odluke da se ista rasprava ne vodi dva puta:

- pretpostavljeni pojmovi, oni koje publika zna bez beleške (aplikacija, HTTP, proces)
- promene konvencija
- terminološke odluke (kad se naziv promeni, a stari ostane alias)
- otvorena pitanja, pojmovi koji još nemaju belešku i kandidati su za naredni čas

### `claude/assets/`

Prazni šabloni iz kojih skill pravi prave beleške: `pojam.md`, `konfiguracija.md`, `odluke.md`, `kontekst.md`. U njima su uglate zagrade i uputstva, ne znanje.

Ne popunjavaju se i ne review-uju kao baza. Ako se pojam doda, fajl ide u `pojmovi/`, ne u `assets/`.

### `claude/SKILL.md`

Uputstvo modelu kako vodi razgovor: kad sme da upiše belešku, kako proverava da definicija nije preširoka ili cirkularna, kada dira kontekst i odluke. Studenti ovde ne dopisuju pojmove.

Vault za skill je folder `claude/`, jer su `_meta/`, `pojmovi/` i `konteksti/` unutra. Pri pokretanju treba reći da koristi postojeću `claude/_meta/konfiguracija.md` i da ne inicijalizuje novu bazu.


## Šta ne ide u repozitorijum

- Slajdovi, beleške za usmeno i bilo šta čime se čas izlaže. To nije baza i ne review-uje se na PR-u.
- Druga konfiguracija pored `claude/_meta/konfiguracija.md`.
- Duplikat pojma zato što se ime fajla razlikuje u slovu. Link u tekstu i ime fajla moraju da budu isti termin.

`assets/` nije višak. To su kalupi. `_meta/` nije višak. Bez njega skill nema temu ni odluke.

## Grane

Jedna grana po prezenteru na jednom času. Na njoj je njegovih oko 10 pojmova, i to je jedan PR.

Nema grane po pojedinačnom pojmu. Deset PR-ova od jedne osobe se ne može pročitati kao celina.

Nema ni jedne stalne grane za ceo čas na koju svi guraju. Tri čoveka u istoj grani gaze jedni druge, a uloga kaže da svaki prezenter dostavlja svoj PR.

Sve grane polaze od `main`. Na `main` stoji baza koja je već prošla čas i integrisana je. Grana živi dok se komentari sa časa ne unesu u beleške i PR ne spoji. Posle spajanja grana se ne nastavlja.

Ako beleška dira samo `pojmovi/`, PR je samo ti fajlovi. Ako primer doda deo sistema, u istom PR-u je i izmena `konteksti/`. Ako se neki termin proglasi pretpostavljenim, u istom PR-u je i `odluke.md`. Konfiguracija se ne otvara bez dogovora celog tima.

Ime grane: `termin1-ime`, na primer `termin1-viktor`.

Prvi čas je izuzetak. Svih 24 pojma nastala su u jednom prolasku i čine jednu celinu. Idu na jednu granu i jedan PR, da urednik i lovac vide ceo skup. Od narednog časa važi pravilo iznad: jedan prezenter, jedna grana, oko 10 pojmova.

## Tok časa

Čas ima tri prezenterа. Svako izlaže oko 10 pojmova, do 20 minuta. Zajedno pokrivaju jednu smislenu celinu tog dana, ne tri nepovezane liste.

PR za bazu stoji 48 sati pre časa, da urednici i lovci stignu da ga prođu. 

1. Prezenter prođe svoje pojmove kroz skill, ili preuzme već napisane beleške ako je prolazak već urađen.
2. Otvori PR. U njemu su markdown beleške, ne prezentacija.
3. Urednik i lovac pročitaju PR pre časa.
4. Na času prezenter izlaže. Urednik kaže šta mora da se ispravi da bi se PR integrisao. Lovac imenuje rupe. Naivni pitalac postavlja pitanja, a PR nije gledao.
5. Posle časa ispravke ulaze u iste beleške, na istu granu. Skill ne menja bazu dok to student ne potvrdi, pa urednik ne prepravlja tuđi fajl umesto prezentera. Kad su ispravke unutra, PR se spaja u `main`.

## Posao po ulozi

### Prezenter (P)

Pre časa napravi ili preuzme svojih oko 10 pojmova i dostavi PR 48 sati ranije. Na času ih izloži za najviše 20 minuta, tako da se sa druga dva prezenterа pokrije celina tog dana. Posle časa unese dogovorene ispravke u beleške i time zatvori PR.

Prezentaciju pravi kako hoće. Nju ne šalje na git.

Za ovaj prvi čas skill je već odrađen: 24 beleške stoje u `claude/pojmovi/`. Prezenter ne pušta te pojmove ponovo kroz skill. Uzme svoj deo, razume definicije i primere dovoljno da ih drugima objasni, i izlaže. Skill se ponovo pokreće samo ako review traži izmenu neke beleške.

### Urednik (U)

Pre časa čita PR tekućih prezentera i već spojene pojmove sa ranijih časova. Gleda da li se definicije slažu: isti termin u dva značenja, cirkularna definicija, primer koji protivreči kontekstu, pojam koji se raspada jer je susedni pojam kasnije promenjen.

Na času proverava da li je izlaganje isto što i beleška. Kaže šta tačno treba ispraviti da bi se PR integrisao. Ne spaja PR pre tog razgovora i ne uvodi tiho svoju formulaciju.

### Lovac na slepe mrlje (L)

Pre časa čita iste PR-ove, ali traži rupe: maglovit termin, link ka belešci koje nema, reč koja bi morala da bude pojam a proglašena je pretpostavljenom, deo problema iz konfiguracije koji pojmovi ne pokrivaju. Lista otvorenih pitanja u `odluke.md` je polazno mesto.

Na času izdvoji najvažnije od toga i kaže zašto taj pojam treba bazi da bi se problem mogao opisati. Ne prepričava ceo PR.

### Naivni pitalac (N)

PR ne otvara i beleške ne čita pre časa. Na izlaganju započinje svaku diskusiju sa bar dva pitanja, uperena u ono što mu je najmaglovitije dok sluša. Zato njegovo pitanje hvata ono što je u tekstu delovalo sređeno, a usmeno se raspadne.

### Slušalac (S)

Prati čas i sprema se da na narednom terminu uzme neku od uloga iznad. Nema fajl koji mora da preda. Može da učestvuje u razgovoru.
