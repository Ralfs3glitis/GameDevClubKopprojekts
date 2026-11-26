# Bullet heaven
## Žanra analīze un produktu izpēte
### Galvenā piesaiste žanram
* Ieguvuma sajūta pēc pietiekama pretinieku skaita iznīcināšanas un līmeņa paaugstināšanas
* Patikamie vizuālie effekti (piem. lietojot uzbrūkumu) kas attiecās uz Aesthetics
### TOP 5 bullet heaven spēles
1. Vampire Survivors
![Vampire Survivors](https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1794680/ss_6c55afe36be2a7784bf18cb9b3218321ae2d10e5.1920x1080.jpg?t=1794307910 "Vampire Survivors")
2. Brotato
![Brotato](https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1942280/ss_6d2f09b839af705c732d4eaf8080a24b9939aca9.1920x1080.jpg?t=1794905667 "Brotato")
3. Halls of Torment
![Halls of Torment](https://shared.fastly.steamstatic.com/store_item_assets/steam/apps/2218750/ss_75fc37b9c2a3b30c01c03d2f3cb86cf6a754ccc2.1920x1080.jpg?t=1792677093 "Halls of Torment")
4. Deep Rock Galactic: Survivor
![Deep Rock Galactic: Survivor](https://shared.fastly.steamstatic.com/store_item_assets/steam/apps/2321470/ss_7580f5af5c21da17f7b19b92ca6c6acf8ffb4776.1920x1080.jpg?t=1793892091 "Deep Rock Galactic: Survivor")
5. Soulstone Survivors
![Soulstone Survivors](https://i0.wp.com/rogueliker.com/wp-content/uploads/2025/05/Soulstone-Survivors-3.jpeg?resize=1024%2C576&ssl=1 "Soulstone Survivors")
### Vampire Survivors Core Loop
1. Spēlētājs nošauj noteiktu priekš līmeņa paaugstināšanas pretinieku skaitu
2. Nākamais līmenis, spelētājs saņem iespēju izvēlēties uzlabojumus priekš nākama līmeņa, kur spēles sarežģītība palielinās; tas ietver sevī gan Reward, gan Expansion aspektus.
### Vampire Survivors MDA
**Gadījumā kad uz spēles kaujas lauka parādas apaļveida pulks pilns ar ienaidniekiem:**
* M - tas events parādās reizi pāris minūtes
* D - spēlētājs koncentrē visu savu uzbrūkumu tieši uz šo pulku
* A - spēlētājs izjūt izaicinājumu, un ieguvuma sajūtu pēc vairāka pretinieku skaita iznīcināšanas
### Spēli taisīja **3** programmētāji
## Veidošana
### Spējas (*Node Slash*, *Node Speed*, *Node Pyro*, *Node Strike*, *Node Shield*, *Node Stun*)
Es veidotu spēju skaita pieaugumu ar katru nākamo līmeni, kā Vampire Survivors
* Bāzes spēja - Slash
* Fire emission
* Šaujamierīce
* Ātrums
* Vairogs
* Enemy stun (varbūt freeze)
### Pretinieki (*Node Creep*, *Node Boss*)
Es palielinātu to HP, pārvietošanas ātrumu un damage ar katru nākamo līmeni, varbūt arī palielinātu to pārvietošanas inerci un samazinātu to projectile pārvietošanas ātrumu prieka pēc (taču realistiski tas izraisīs problēmas ar optimizāciju). Pretinieki būs:
* **Creep** - izdara damage tikai kad saduras ar spēletāju, sākotnējais HP = 15,
* **Boss** - izdara damage no attāluma, lielāks HP un rētāk sastopams, sākotnējais HP = 150.
### Spēlētājs (*Node Bomber*, *Node Cowboy*)
Divas opcijas (un speciālās spējas):
* **Bomber** - lek uz priekšu un izdara DMG visiem pretiniekiem noteiktā radiusā,
* **Cowboy** - iemet laso un notur tajā pretiniekus, lai tie paliktu ka liels gabals, nevis aizbegtu pa kaujas lauku.
### Spēlētāja rādītāji (*Resource Stats*)
* Dzīvības (HP) - lai sabalansētu spēli, `Bomber.HP = 160 > Cowboy.HP = 100` un HP ir integer
* Krit. iespēja - kaut kur ap 12%
* Krit. DMG - no 4 līdz 30 ar nejauši ģenerēto skaitli tajā intervālā
* Pretinieku veidošanas - Uzreiz ekrānā nedrīkst būt vairāk par 50 pretiniekiem, tie parādās ārpus ekrāna kaujas laukā
* Ievainojums (DMG) - sākotnējais DMG ir no 1 līdz 15 ar nejauši ģenerēto skaitli tajā intervālā
* Pieredze un jauna līmeņa iegūšana - jauno līmeni iegūst, iznīcinot **Boss**, kas no sākuma parādās tikai kad spēlētājs iznīcināja 9 pretiniekus
* Jauno spēju atbloķēšana - jaunas spējas var iegūst reizi 2 līmeņa paaugstināšanas. Paaugstinot līmeni, parādās logs ar 3 spēju izvēlēm, kur izvēlēties var tikai 1 no tiem.
## Pseidokods
```
sākums
  spawn player
  spawn enemies
  atkārtot
    ja iznīcināti 8 enemy
      spawn boss
      ja boss ir iznīcināts
        level up
  kamēr player.HP != 0
  citādi you died
beigas
```
