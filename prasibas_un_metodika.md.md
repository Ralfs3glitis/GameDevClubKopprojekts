# Kopīgi programmēta spēle "datorspēļu dizains un programmēšana" pulciņa ietvaros
Galvenā piesaiste žanram ir tāds kā tu ar katru jaunu wave vai round paliec stiprāks un sāk vairāk galvenāt pretiniekus, bet viņi arī paliek daudz un stiprāki tad tu nomirsi, bet lobby vari dabut labākas mantas vai nopirt passive perk, kas tev palīdzēs tikt tālak nekā iepriekš tu tiki.
1. Soulbound: Online
   ![Spele](https://shared.fastly.steamstatic.com/store_item_assets/steam/apps/4369490/11785a509fe5f4818f307d54a6ec331c16669fc0/page_bg_raw.jpg?t=1795188542)
2. God of forsaken
   ![spele]([https://imagedelivery.net/0L7Z8leoZRtgqeObGMDoKQ/aa51b3fb-bc8d-4c9e-8a5d-429c14c9c400/public](https://images.steamusercontent.com/ugc/12830131513973357211/CED7F6C9CB58011875C097E7B8C7D6510FD97BE1/?imw=1024&&ima=fit&impolicy=Letterbox&imcolor=%23000000&letterbox=false))
3. Vampire Survivors
   ![spele](https://img.itch.zone/aW1hZ2UvMTI0MjQ2OC83MjY2MjYzLnBuZw==/original/40BKlP.png)
4. Brotato
   ![spele](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTQMLMLtiMGr5O7XP23sOhSGL4MakvmokC3pVFr0VOzF2sPqGkbWwDXDc25&s=10)
5. Deep Rock Galactic survivors
  ![spele](https://shared.fastly.steamstatic.com/store_item_assets/steam/apps/2321470/ss_7580f5af5c21da17f7b19b92ca6c6acf8ffb4776.1920x1080.jpg?t=1793892091)
6. The binding of Isaac
   ![spele](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR8XF232KG_C_UQyqXh3ljn7qvHUzpHryJSqeg_e1LEfY-VOH2pK7lGrBiP&s=10)

## The binding of Isaac analīze
---
Spēles coor loop: Spēles coor loop ir galināt bosus atbloķējot jaunus priekšmetus un kad pabeidzas run tad sāc jaunu un vai nu izvēlies citu bossu vai izvēlies citu character, lai no viņa atbloķet jaunus priekšmetus un tā reiz pa reizei kāmēr neatver visus priekšmetus un nesaņem visus achievment

Spēles MDA: Spēle ir grūts boss kuru paveikt ir grūti ar parastiem priekšmetiem ar reitingu T1 līdz T2, bet ja paveicas vari dabūt labākus priekšmetus līdz T3-T4 un tad tev bossu būs vieglāk paveikt. Spēlētājam atšķirība no iegūtiem priekšmetiem un cik viņi ir efektīvi savā starpā saprot cik grūti būs paveikt šo bossu vai vispār nav jēgas iet uz viņu. Spēlētājs sāk reaģēt uz priekšmetiem, jo sliktāks priekšmets jo negatīvāka reakcija, jo būs grūtāk paveikt bossu, bet ir izņēmumi ar  spēlētājiem, kas meklē piedzīvojumus un speciāli cenšās apgrūtināt savu run.

Bonusa jautājums cik cilvēku veidoja šo spēli?
---
Šo spēli veidoju 2 cilvēki, ja pieskaitot komponistu tad 3, vēlāk kad spēli pārbūvēja uz jaunākā dzinēji tad komanda izauga līdz 10-15 cilvēkiem.

# Kā es veidotu šo žanra spēli??

### Spējas

Spējas es veidotu izveidojot godot project settingos specializēto keybind, kas atbild par to. Tad player scripta es norāditu pie darbībām kad tiek nospiests tas taustiņš, kas tieši notiktu, piem, iedarbotos ar playaer statistiku atņemot viņa mana, vai tam līdzīgs. Spējām atšķirība cik viņas pēc mehanikas ir labas vai sliktas uztaisītu cooldown cik bieži var izmantot. Varbūt var spēja būt kā passive skill kuru tu iegūst, kad characters iegūst level up vai saņem kā reward. Spēja ietekmetu kā uz character tā arī uz apkārtējo vidi.

- es izmantotu animacijas mezglu, lai animētu spēja, ja tā nav passīva. Tiktu izmantots ari area 2d lai reaģetu ar vidi būtu arī shape mezgls, lai spējai iedotu formu.
- Es izmantotu resursu spējas buff vai viņu dmg ko dara jeb spējas specifikācijas, kuras varētu ietekmēt arī citas spējas vai priekšmeti.
- Piemērām spējas FireBall:
     ``` text
     Spēletājs uzspiež uz c
     spēle aktivizē skripta funkciju
     parādas fireball
     lido noteikto distanci
     ja trapa ienaidnieka tad
     vinam atnemas momentāli hp un vel fire dmg uz dazam sekundēm
     citadi fireball palido garam un tad pazūd pēc noteiktām sekundēm.
     ```
### Pretiniekus

- es izmantotu animācijas mezglu, shape mezglu, area 2d mezglu un arī player mezglu, lai varētu interaktot labāk ar apkārti.
- Es izmantotu resursus pretiniekam, resurs būtu izmantot priekš spējam, pretinieka parametriem un pretinieka ieročiem.
- Piemēram pretinieka uzbrukums:
   ``` text
   Pretinieks pamana spēlētāju
   pretinieks iet uz spēlētāja pusi apejot garām šķēršļus
   kad pretinieks ir pietiekoši tuvu spēlētajam viņš sāk uzbrukt
   pretinieks iesit spēlētājam
   pagaidā mazu brīdi
   ja spēlētajs ir uzbrukuma zonā tad sit atkal
   citādi pretinieks iet klāt spēletājam, ja pretinieks vel ir dzīvs
   ```
### Spēlētājs

- es izmantotu player mezglu, shape mezglu un area2d mezglu, lai varētu ietekmēt ar apkārtni arī animācijas mezglu.
- es izmantotu resursus, spēlētaju spējam, ieročiem viņu parametriem cik hp un mana? un vēl kaut kas, arī izmantotu resursu priekš čaraktēra tēla, lai spēlētājs izvēlas savam characteram to tēlu ko viņš grib.
- iespēju izvēleties tēlu:
   ``` text
   Spēlētājs ir startējis spēli
   Viņam piedāva izvēleties tēlu savam spēlētājam
   spēletājs izvēlas vienu no tēliem
   spēle saglabā spēlētaju izvēli resursā
   turpmāk spēle izmantos tieši ša spēlētāju izvēli un rādīs viņa tēlu
   ```

### Spēlētāju rādītāji

- spēletāju rāditājam vairāk kārt nevajag mezglus vienīgais varētu izmantot UI mezglus, lai attēlot viņu rādītājus, piem, ka **The Binding of the Isaac** kur tu ieslēdz iestatījumos, lai parāda tava tēla rādījumus.
- es izmantotu resursu gandrīz visu spēlētāju rādītājiem, lai kad mēs pārejam jaunajā ainā pārnestos rādījumi.
- piemeram:
  ``` text
   Spēlētaju rādijumi
  pāriet uz citu ainu
  spēlētājam piešķier tos resursus, kas bija iepriekš
  ```

### Pretinieku veidošanas (spawning)

- Pretinieku veidošanam es izmantotu tikai area 2d mezglu, kur ja speletajs ir iegajis vai vina tur nav pretinieks var sākt veidoties pēc skripta nosacījumiem.
- Nē, pretinieku veidošanam nevajdzētu izmantot resursu veidošanai
-  piemēram:
   ``` text
   Spēlētājs ienāk pretinieku zona
   area 2d atnāk signāls, ka tieši spēletajs ienaca
   scripts ar pretinieku veidošanu sāk inicializēties
   pretinieki sāk parādities uz mapes
   ```

### Pieredze un jaunu līmeņa iegūšanu

- es izmantotu ui mezglus, lai ainās attēlu spelētaju pieredzi vai viņu tekošo līmeni vai kad viņš iegūst jaunu līmeni
- Es izmantotu resursu tikai, lai saglabātu līmeņu stāvokli un pārnest uz citu ainu
- piemēram:
  ``` text
  Spēletājs ieguva nepieciešamo pieredzu skaitu
  Spēle iedot spēletājam jaunu līmeni
  Spelētājs sāk krāt pieredzi uz jaunu līmeni
  ```

### Jaunu spēju atbloķēšana

- es izmantotu ui mezglus, lai parādīt kādas spējas ir pieejamas izvēlei, spēletājam kad sasndiedz jaunu līmeni
- Resursus es neizmantotu
- piemērs:
  ``` text
  Spelētājs sasniedz jaunu līmeni
  Spēle parāda trīs kartītes kurā ir attēlota spēja un aprakstīts ko viņi dara
  spēlētajs uzkliskina vienu no kartītēm
  pēc spēlētāja izvēles spēle piešķir viņam izvelēto speju
  spēletājs ieguva spēju
  spēlētājs spēle ar jaunu spēju
  ```
