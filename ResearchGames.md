### Bullet heaven žanra pētniecība.

Kāda ir galvenā piesaiste žanram?
- Varas fantāzija par neapturamību


Kādas ir 5 populārākās šī žanra spēles?
- Vampire Survivors,
<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/e9abf267-5519-449b-9716-558852c23fc3" />

- Brotato,
<img width="1200" height="628" alt="image" src="https://github.com/user-attachments/assets/d0875039-6418-4b25-8109-f28f2e015699" />

- Survivor.io,
<img width="887" height="531" alt="image" src="https://github.com/user-attachments/assets/5e446527-9ca7-4c32-a4b3-8b77d2f45e43" />

- 20 Minutes Till Dawn,
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/55c1181d-dc3a-47db-9a41-7be7a8b205c5" />

- Megabonk
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f0627483-2d42-4b43-86fa-d98009d4ee93" />


Izvēlies vienu no spēlēm, un analizē:
- 20 Minutes Till Dawn


Spēles Core Loop
- Cīnies -> Iegūsti pieredzi -> Paaugstini līmeni -> Kļūsti spēcīgāks -> Izdzīvo


Vienu no tās mehāniku MDA framework (pēc izvēles)
- M: Spēlētājs pats tēmē un šauj ar ieroci. Munīcija ir ierobežota, tāpēc ierocis ir jāpārlādē.
- D: Spēlētājam jāizvēlas, kad šaut un kad pārlādēt, vienlaikus izvairoties no monstriem.
- A: Šī mehānika rada spriedzi, izaicinājumu un gandarījumu, kad izdodas iznīcināt lielu monstru grupu.


Bonuss - jautājums: cik cilvēki veidoja spēli?
- Flanne (solo izstrādātājs).


### Kā es taisītu šādu spēli?

- Spējas

Spēlē tiktu izmantotas tikai dažas universālas uzbrukumu bāzes ainas (Scene), piemēram, Projectile šāviņiem un MeleeHitbox tuvcīņas sitieniem. Katra konkrētā uzbrukuma unikālie parametri — bojājumi (Damage), ātrums, darbības rādiuss, animācija, šāviņu skaits un papildu efekti — tiktu glabāti atsevišķā AttackData (Resource) failā. Uzbrukuma brīdī universālā bāzes aina ielādētu attiecīgā Resource datus, piemērotu nepieciešamo vizuālo izskatu un ar Area2D un CollisionShape2D noteiktu trāpījumus pretiniekiem.

- Pretinieki

Visi pretinieki tiktu veidoti uz vienas kopīgas bāzes ainas (Unit.tscn) pamata, kuru konfigurē atsevišķi UnitData (Resource) faili (izskats, dzīvības punkti, pārvietošanās ātrums un pieejamais AttackData). Lai nodrošinātu augstu veiktspēju lielam pretinieku skaitam, pretinieki izmantotu vieglus Area2D mezglus un to kustība tiktu aprēķināta tieši kodā (position += direction * speed * delta), savukārt savstarpējā grūstīšanās tiktu risināta ar vienkāršu attāluma pārbaudi starp tuvākajiem pretiniekiem. Katrai vienībai būtu maināms vadības komponents — parastā režīmā to vada AIController, bet pārņemšanas brīdī vadība tiek pārslēgta uz PlayerController.

- Spēlētājs

Spēlētājs vada mazu parazītu (Node2D ar AnimatedSprite2D), kuram pašam nav tiešu uzbrukuma spēju. Nospiežot un turot Space taustiņu, tiek parādīta mērķēšanas trajektorija peles kursora virzienā. Atlaižot taustiņu, parazīts patērē noteiktu daudzumu asiņu un veic ātru lēcienu uz izvēlēto punktu:
Veiksmīgs trāpījums: Ja lēciena galapunktā atrodas pretinieks, parazīts piesaistās tam kā saimniekam (Host), pārslēdz tā vadību uz PlayerController un ļauj spēlētājam izmantot šī pretinieka kustību un uzbrukumus.
Netrāpīts lēciens: Ja parazīts piezemējas tukšā vietā bez saimnieka, tas paliek uz zemes bez iespējas aizstāvēties bet ar spēju pārvietoies, kamēr pretinieki turpina tam nodarīt bojājumus, līdz tiek pie jauna saimnieka.

- Spēlētāja parametri

Spēlētājam nav atsevišķas dzīvības un enerģijas joslas — ir viens kopīgs resurss asinis (Blood), kas vienlaikus kalpo gan kā dzīvības punkti, gan kā maksa par lēcieniem uz jauniem saimniekiem. Saņemot bojājumus (īpaši atrodoties uz zemes bez saimnieka) vai veicot lēcienu, asiņu daudzums samazinās, un, tam sasniedzot nulli, spēle beidzas. Papildus tam spēlētājam ir arī citi parametri, piemēram, kritiskā trāpījuma iespējamība (Crit Chance), kritiskā trāpījuma bojājumi (Crit Damage), uzbrukumu spēks (Might / Power), lēciena attālums un asiņu ieguves apjoms. Visi šie bāzes parametri tiek glabāti ParasiteStats (Resource) failā, un mēģinājuma (Attempt) sākumā tiek izveidota tā kopija ar duplicate(), lai spēles laikā iegūtie uzlabojumi ietekmētu tikai konkrēto mēģinājumu un automātiski tiktu nodoti jebkuram pārņemtajam saimniekam.

- Pretinieku veidošanās

Lai izvairītos no liekas atmiņas noslodzes, nepārtraukti izveidojot un dzēšot mezglus spēles laikā, spēlē tiktu izmantots Object Pooling princips. Līmeņa sākumā tiktu iepriekš izveidots noteikts skaits neaktīvu Unit ainu. Pēc Timer noteikta intervāla (atkarībā no grūtības pakāpes Resource datiem) viens no neaktīvajiem pretiniekiem tiktu aktivizēts nejaušā vietā aplī ap spēlētāju ārpus redzamības zonas, aprēķinot koordinātas ar randf_range(), sin() un cos() funkcijām, un konfigurēts ar attiecīgo UnitData resursu. Kad pretinieka dzīvības punkti sasniedz nulli, tas netiek izdzēsts, bet gan paslēpts un atgriezts neaktīvo objektu kopā (Pool) atkārtotai izmantošanai.

- Pieredze un līmeņu iegūšana

Nogalinot pretiniekus, to atrašanās vietā tiktu izveidoti asiņu pilieni (Blood Orb), kurus pārvaldītu viens centralizēts BloodManager skripts (izmantojot vieglus Sprite2D vai MultiMeshInstance2D mezglus). Tas vienā ciklā pārbaudītu attālumu (distance_squared_to()) līdz spēlētājam, ar move_toward() pievilktu tuvākos pilienus un pieskaitītu asinis spēlētāja krājumiem.
Līmeņa paaugstināšana: Savāktais asiņu daudzums uzkrājas kopējā pieredzes progresā. Sasniedzot nākamajam līmenim nepieciešamo slieksni, lietotāja saskarnē (Control mezgli) spēlētājam tiek piedāvāti trīs nejauši izvēlēti uzlabojumi (UpgradeData resursi).
Uzlabojumu darbība: Izvēlētais uzlabojums pievieno jaunu pasīvu efektu spēlētāja ParasiteStats parametru sarakstam. Katru reizi, kad parazīts pārņem kādu saimnieku, šie uzlabojumi automātiski tiek nodoti pārņemtā saimnieka uzbrukumiem (piemēram, pievienojot indes bojājumus, lielāku uzbrukuma ātrumu, kritiskā trāpījuma iespēju vai sprādzienu pēc pretinieka nogalināšanas).

- Jaunu spēju atbloķēšana
Sasniedzot noteiktu līmeni, spēlētājs atbloķētu jaunas parazīta spējas (piemēram, triecienvilni piezemēšanās brīdī vai īslaicīgu paātrinājumu pēc saimnieka pamešanas), kuras var izsaukt jebkurā mēģinājuma brīdī ar Input sistēmu, nospiežot tām piešķirto taustiņu. Katras spējas parametrus (atbloķēšanas līmeni, bojājumus, atkārtotas izmantošanas laiku un vizuālos efektus) glabātu atsevišķā AbilityData (Resource) failā, bet pašai spējas izpildei izmantotu tās pašas universālās bāzes ainas (piemēram, AreaEffect vai Projectile), savukārt atkārtotas izmantošanas laiku (Cooldown) kontrolētu ar Timer.
