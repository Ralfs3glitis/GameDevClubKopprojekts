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

Spējas aina (Scene) tiktu izveidota spēlētāja atrašanās vietā un atskaņotu savu animāciju. Izmantojot Area2D un CollisionShape2D, tiktu noteikti pretinieki, kas atrodas spējas darbības zonā. Noteiktā animācijas kadrā ar AnimationPlayer palīdzību tiktu izsaukta funkcija, kas nodarītu bojājumus (Damage) visiem attiecīgajā zonā esošajiem pretiniekiem un radītu nepieciešamos efektus. Katras spējas aina tiktu saglabāta kā PackedScene, savukārt tās parametrus, piemēram, bojājumus un darbības rādiusu, varētu glabāt atsevišķā Resource.

- Pretinieki

Pretinieki būtu kolīzijas objekti, kuri nevarētu iziet cauri cits citam. Izmantojot CharacterBody2D un CollisionShape2D, tiktu nodrošināta to kustība un sadursmju noteikšana. Katrā kadrā pretinieki ar move_and_slide() funkciju virzītos spēlētāja pozīcijas virzienā, ņemot vērā savu kustības ātrumu. Katram pretiniekam būtu noteikts dzīvības punktu daudzums, kas tiktu glabāts tā parametros. Kad dzīvības punktu skaits sasniegtu nulli vai kļūtu mazāks par to, pretinieks tiktu izņemts no spēles ainas, izmantojot queue_free() funkciju. Pretinieku ainas tiktu saglabātas kā PackedScene, bet to parametrus, piemēram, dzīvības punktus, ātrumu un bojājumus, glabātu Resource.

- Spēlētājs

Spēles galvenajā izvēlnē spēlētājam būtu iespēja izvēlēties spēlējamo personāžu, izmantojot pogas, kā arī iespēja mainīt tā tēlu pirms mēģinājuma (Attempt) sākšanas. Katram personāžam būtu savi bāzes parametri (Base Stats), kurus varētu uzlabot ar uzlabojumiem (Upgrades) vai kuriem jau sākotnēji būtu piešķirti īpaši uzlabojumi. Spēlētāja kustību nodrošinātu CharacterBody2D, savukārt tēla animācijas kontrolētu AnimatedSprite2D vai AnimationPlayer. Spēlētājs izmantotu standarta kustību vadību un taustiņu piesaistes (Keybinds) spēju aktivizēšanai, kā arī peli ieroča vadībai, ja ierocis nebūtu pasīvs. Katra personāža sākotnējos parametrus un izskatu varētu glabāt atsevišķā Resource, bet pašu personāžu ainas — kā PackedScene.

- Spēlētāja parametri

Spēlētājam būtu dažādi parametri, piemēram, dzīvības punkti (Health), kritiskā trāpījuma iespējamība (Crit Chance), kritiskā trāpījuma bojājumi (Crit Damage) un spēju un ieroču spēks (Might / Power). Mēģinājuma sākumā tiktu izveidota spēlētāja sākotnējo parametru kopija, izmantojot Resource un tā duplicate() funkciju, uz kuras pamata tiktu piemēroti turpmāk iegūtie uzlabojumi. Tādējādi spēlētāja sākotnējie parametri paliktu nemainīgi, bet mēģinājuma laikā iegūtie uzlabojumi ietekmētu tikai konkrēto mēģinājumu. Piemēram, iegūstot uzlabojumu, kas palielina kritiskā trāpījuma iespējamību, attiecīgā vērtība tiktu pieskaitīta spēlētāja pašreizējam parametram.

- Pretinieku veidošanās

Pēc noteikta laika intervāla, kas būtu atkarīgs no grūtības pakāpes (Difficulty), spēles ainā tiktu izveidots jauns pretinieks. Pretinieka atrašanās vieta tiktu izvēlēta nejauši aplī ap spēlētāju, ievērojot minimālo un maksimālo attālumu no spēlētāja. To varētu panākt, ģenerējot nejaušu leņķi un attālumu, izmantojot randf_range(), un aprēķinot jaunās pozīcijas koordinātas ar sin() un cos() funkcijām. Šajā nejauši izvēlētajā pozīcijā tiktu izveidota pretinieka aina, izmantojot PackedScene un instantiate() funkciju. Pretinieku veidošanās intervālus kontrolētu Timer, savukārt grūtības pakāpes parametrus, piemēram, veidošanās biežumu un pretinieku veidus, glabātu atsevišķā Resource.

- Pieredze un līmeņu iegūšana

Pirms pretinieks tiktu izņemts no spēles ainas, tā atrašanās vietā tiktu izveidots pieredzes objekts (Experience Orb), izmantojot atsevišķu PackedScene. Kad spēlētājs pietuvotos pieredzes objektam līdz noteiktam attālumam, tas sāktu virzīties spēlētāja virzienā, izmantojot attāluma pārbaudi un move_toward() funkciju. Kad objekts pieskartos spēlētājam, izmantojot Area2D un CollisionShape2D, tas tiktu absorbēts un piešķirtu pieredzes punktus (EXP). Līmeņa paaugstināšanai nepieciešamais pieredzes punktu daudzums palielinātos pēc pakāpeniskas formulas. Kad spēlētājs sasniegtu nākamajam līmenim nepieciešamo pieredzes punktu daudzumu, no pašreizējās pieredzes tiktu atņemts nepieciešamais daudzums un spēlētāja līmenis paaugstinātos. Katru reizi, kad spēlētājs iegūtu jaunu līmeni, viņam tiktu piedāvāti trīs nejauši izvēlēti uzlabojumi, izmantojot Control mezglus lietotāja saskarnes izveidei. Spēlētājs varētu izvēlēties vienu no tiem, un izvēlētais uzlabojums vai nu mainītu spēlētāja parametrus, vai arī piešķirtu jaunu efektu, kas aktivizētos, iestājoties noteiktam nosacījumam. Piemēram, kritiska trāpījuma gadījumā varētu notikt sprādziens, izveidojot attiecīgo efektu ainu.

- Jaunu spēju atbloķēšana

Sasniedzot noteiktu līmeni, spēlētājs atbloķētu jaunu spēju, kuru pēc tam varētu izsaukt jebkurā mēģinājuma brīdī, izmantojot tai piešķirto taustiņu. Spēlētāja līmenis tiktu salīdzināts ar katras spējas atbloķēšanas līmeni, un, sasniedzot nepieciešamo līmeni, attiecīgā spēja tiktu pievienota spēlētāja pieejamo spēju sarakstam. Izmantojot Input sistēmu, tiktu pārbaudīts, vai spēlētājs nospiež attiecīgajai spējai piesaistīto taustiņu. Ja spēja būtu atbloķēta un tās atkārtotas izmantošanas laiks (Cooldown) būtu beidzies, tiktu izveidota attiecīgā spējas aina spēlētāja atrašanās vietā. Katras spējas ainu glabātu kā PackedScene, bet tās parametrus, piemēram, atbloķēšanas līmeni, bojājumus un atkārtotas izmantošanas laiku, — kā Resource. Spēju atkārtotas izmantošanas laiku varētu kontrolēt ar Timer.
