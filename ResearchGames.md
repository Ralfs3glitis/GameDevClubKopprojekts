###Bullet heaven žanra pētniecība.###
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


###Kā es taisītu šādu spēli?###
Spējas
Scnēna kura izveidota spēlētāja lokācijā un izspēlē savu animāciju - darot damažu un effektus būtnēm grupā pretenieki noteiktā freimā.

Pretiniekus
Kolīzijas objekti kas nevar iziet caur viens otram un katru frameu tiks Lerpots uz spēlētāja pozīciju attālumu balstoties uz to ātrumu. Tiem būtu noteikts daudzums dzīvības kura, kad viņiem butu vienāda ar 0 vai mazāka, liktu viņiem savi noņemt no spēles scēnas.

Spēlētāju (ar iespēju mainīt tēlu)
galvenajā ciltē, pirms attempta sākšanas, spēlētājam būtu spēja ar pogām izvēlēties spēlējamu personāžu kas notiektu tā bazes status kurus upgreidi uzlabotu, vai nāktu ar iebūvētiem upgreidiem. Spēlētājs varētu lietot standarta kustību un keybindus priekš spējām / mouse priekš ieroča (ja tas nav passīvs).

Spēlētāja rādītājus (stats), piem. dzīvības, crit chance, crit damage, might / power.
resurs kurus nokopē attempta sākuma un uz kuriem pa virsu tiek applyoti upgreidi.

Pretinieku veidošanos (spawning)
kad paiet notiekts laika daudzums, balstoties uz difficulty, noteiktā distancē (min attālums + max attālums) no spētāja, random pozīcijā aplī ap spēlētāju tiktu izveidota pretenieka scena. 

Pieredzi un jaunu līmeņu iegūšanu
pirms preteniks noņem sevi no scenas, tas izveido pieredzes scenu. pierredzes scena tiek pievilka pie spēlētāja kad tas ir pietiekami tuvu un absorbēta kad tas pieskaras tam. balsoties uz inkrementālu formulu vajadzētu veirāk un vairāk exp lai palielinātu līmeni. katru reizi kad līmenis palielinas (kad exp sasniedz lvup threshold un tiek resetots), spēlētājam piedāvā vienu no 3 upgreidiem. Izvēlētais upgreids izpilda savu effektu uz tā statiem / tiek izveidots kad notiek kondīcija (piemēram sprādziens kad izdara crit dmg).

Jaunu spēju atbloķēšanu
sasniedz lv threshold un tiek iegūta spēja summonot to scēnu.

Katram:
Kādus mezglus izmantotu?
Vai izmantotu resursus? Kam?
Apraksti galveno loģiku pseidokodā.
