# Kopīgi programmēta _bullet heaven_ spēle "datorspēļu dizains un programmēšana" pulciņa ietvaros

## Kā strādā mūsu sistēma

Mums ir **viens kopīgs GitHub repozitorijs**. Visi dalībnieki saņem tiesības to noklonēt un veidot savus zarus. Tāpēc pulciņa laikā vari strādāt patstāvīgi savā zarā, netraucējot citiem.

### Zari

**Zars** (*branch*) ir paralēla projekta versija. Tajā vari brīvi eksperimentēt un nesabojāsi ne citu darbu, ne oficiālo versiju.

| Zars            | Kam pieder        | Kam paredzēts                                                                                           |
| --------------- | ----------------- | ------------------------------------------------------------------------------------------------------- |
| `main`          | Pulciņa vadītājam | Oficiālais stāvoklis. Katras nodarbības beigās šeit tiek ievietots viss, kas nodarbībā bija jāsasniedz. |
| `Vards_Uzvards` | Tev               | Tavs personīgais zars, kurā strādā patstāvīgi savā tempā.                                               |

Zari izskatās apmēram šādi:

```text
main     o───────────o───────────o───────────o───▶  pulciņa vadītājs (pēc katras nodarbības)
         │
         ├──o──o──o──o──o──o──o──o───────────────▶  janis-berzins
         │
         └──o──o──o──o──o────────────────────────▶  anna-kalnina
```

Katrs strādā savā zarā, tāpēc **neviens nevar sabojāt cita darbu**. Visus zarus vari redzēt GitHub lapā, nospiežot zara izvēlni (tur, kur rakstīts `main`).

### Nodarbību cikls

1. Nodarbībā kopā apskatām jauno tēmu.
2. Katrs to īsteno **savā zarā**, savā tempā.
3. Nodarbības beigās es `main` zarā ievietoju visu, kas nodarbībā bija jāsasniedz.
4. Ja kaut ko neizdevās vai izlaidi nodarbību, vari sākt no `main` - skat. [Ja atpaliec vai izlaid nodarbību](#ja-atpaliec-vai-izlaid-nodarbību).

### Terminu vārdnīca

| Termins | Ko tas nozīmē |
|---|---|
| **repozitorijs** (*repository*) | Projekta mape kopā ar visu tā izmaiņu vēsturi, kas glabājas GitHub |
| **klonēt** (*clone*) | Pirmoreiz lejupielādēt repozitoriju savā datorā |
| **zars** (*branch*) | Paralēla projekta versija, kurā vari strādāt netraucēti |
| **commit** | Izmaiņu saglabāšanas punkts ar īsu aprakstu - kā "saglabāšanās punkts" spēlē, pie kura vienmēr var atgriezties |
| **push** | Nosūtīt savus commit uz GitHub |
| **pull** | Lejupielādēt jaunākās izmaiņas no GitHub un ieviest tās savā zarā |
| **merge** | Apvienot viena zara izmaiņas ar cita zara izmaiņām |
| **konflikts** | Kad Git nezina, kuru no divām atšķirīgām izmaiņām paturēt, un tev jāizvēlas pašam |

## Darba sākšana

### Kas vajadzīgs

- [GitHub Desktop](https://github.com/apps/desktop) (iesācējiem) vai [Git](https://git-scm.com/) (profiņiem);
- [GitHub](https://github.com/) konts ar piekļuvi šim repozitorijam (apstiprini uzaicinājumu, ja saņēmi e-pastu);
- [Godot](https://godotengine.org/) - tā pati versija, ko lietojām līdz šim.

### 1. Noklonē repozitoriju (tikai vienu reizi)

Repozitorija adresi atradīsi GitHub lapā zem zaļās **Code** pogas.

```bash
git clone https://github.com/Ralfs3glitis/GameDevClubKopprojekts.git cloned-repo
cd cloned-repo
```

Pēc klonēšanas tu atrodies `main` zarā. Tajā **nestrādā** - vispirms izveido savu zaru.

### 2. Izveido savu zaru

```bash
git switch -c Vards_Uzvards
```

Zara nosaukumam veido diakritiskajām zīmēm (ā, č, ģ, š u.c.); vārdus atdali ar apakšsvītru. Piemēri: `Janis_Berzins`, `anna_kalnina`.

Lai pārliecinātos, kurā zarā esi, izpildi `git branch` - aktīvo zaru atzīmē ar `*`.

### 3. Atver projektu Godot

Godot projektu pārvaldniekā spied **Import** un izvēlies failu `project.godot` no noklonētās mapes.

## Ikdienas darba cikls

Kamēr strādā, atkārto šo ciklu:

1. Strādā Godot un pārbaudi, vai spēle darbojas.
2. Saglabā failus Godot (`Ctrl+S`) - Git redz tikai saglabātos failus.
3. Saglabā progresu ar Git:

```bash
git status                       # kas mainījies un kurā zarā esmu?
git add .                        # sagatavo visas izmaiņas
git commit -m "Īss apraksts"     # saglabā tās vēsturē (commit)
git push                         # nosūta uz GitHub
```

> [!NOTE]
> Pirmajā reizē, kad savu zaru sūti uz GitHub, jālieto garākā komanda ar sava zara nosaukumu: `git push -u origin vards_uzvards`. Pēc tam pietiek ar `git push`.

### Labs commit

- Veic commit **bieži** - pēc katra neliela darba, kas strādā. Tas ir tavs *checkpoint*: ja kaut kas noiet greizi, vari atgriezties.
- Apraksti, **ko izdarīji**. 
  Labi: `Pievienots pretinieku object pool`. 
  Slikti: `izmaiņas`, `asdf`, `labojums`.

## Ja atpaliec vai izlaid nodarbību

Nekas nav zaudēts! `main` zarā vienmēr ir oficiālais nodarbību rezultāts, un no tā vari sākt jebkurā brīdī.

| Situācija | Ko izvēlēties |
|---|---|
| Izlaidu nodarbību vai gribu sākt no oficiālā rezultāta | **A variants** |
| Gribu paturēt savu darbu un pievienot tam nodarbības rezultātu | **B variants** |
| Viss sajaucies un nesaprotu, kas notiek | **C variants** |

> [!IMPORTANT]
> Pirms sāc: aizver Godot un pārliecinies, ka viss tavs darbs ir saglabāts. `git status` jāpasaka *nothing to commit, working tree clean*. Ja nav - veic commit vai atmet izmaiņas ar `git restore .`.

### A variants: jauns zars no `main`

Tavs vecais zars paliek neskarts, bet jaunais sākas no oficiālā nodarbības rezultāta.

```bash
git switch main                  # pārslēdzies uz main
git pull                         # lejupielādē jaunākās izmaiņas
git switch -c vards_uzvards_2    # izveido jaunu savu zaru no main
```

Pirmajā nosūtīšanas reizē lieto `git push -u origin vards_uzvards_2`.

### B variants: pievieno `main` izmaiņas savam zaram

Ja gribi paturēt savu darbu un papildus iegūt nodarbības rezultātu:

```bash
git switch vards_uzvards         # pārslēdzies uz savu zaru
git fetch origin                 # uzzini, kas jauns GitHub
git merge --no-edit origin/main  # apvieno main izmaiņas ar savu zaru
```

Ja abi esat mainījuši vienus un tos pašus failus, Git var ziņot par **konfliktu**. Failā tas izskatās šādi:

```text
<<<<<<< HEAD
tas, kas ir tavā zarā
=======
tas, kas ir main zarā
>>>>>>> origin/main
```

Atstāj to, kas vajadzīgs, un izdzēs atzīmes :
```
<<<<<<<, ==========, un >>>>>>>
``` 
Tad pabeidz apvienošanu:
```bash
git add .
git commit --no-edit
```

> [!TIP]
> Konflikti Godot ainu failos (`.tscn`) ir grūti salasāmi. Ja kļūst par sarežģītu - atcel apvienošanu ar `git merge --abort` un izmanto A variantu.

### C variants: sāc no tīras lapas

Vienkāršākais variants, ja nekas nesanāk - noklonē `main` vēlreiz jaunā mapē:

```bash
cd ..                            # iziet no pašreizējās projekta mapes
git clone https://github.com/Ralfs3glitis/GameDevClubKopprojekts.git bullet-heaven-jauns
cd bullet-heaven-jauns
git switch -c vards_uzvards_2
```

## Noteikumi

> [!IMPORTANT]
> **`main` zarā nestrādājam un uz to nesūtām `push`** - tur lieku nodarbību rezultātus.

1. Katram savs zars, nosaukts `vards_uzvards`.
2. Neaiztiec citu dalībnieku zarus.
3. Pull request veidot nav nepieciešams - katrs strādā savā zarā.
4. Veic commit bieži un apraksti, ko izdarīji.
5. Eksperimentē drosmīgi! Savā zarā tu netraucē nevienam, un vari atgriezties pie pēdējā commit.
6. Iestrēdzi? Pamēģini `git status` - tas bieži pasaka, kas notiek un ko darīt tālāk. Ja neizdodas, jautā!
## Git špikeris

| Komanda | Ko dara |
|---|---|
| `git clone <adrese>` | Noklonē repozitoriju savā datorā |
| `git branch` | Parāda zarus (`*` = tavs pašreizējais) |
| `git status` | Parāda, kas mainījies un kurā zarā esi |
| `git switch -c <zars>` | Izveido jaunu zaru un pārslēdzas uz to |
| `git switch <zars>` | Pārslēdzas uz esošu zaru |
| `git add .` | Sagatavo visas izmaiņas commit veikšanai |
| `git commit -m "apraksts"` | Saglabā izmaiņas vēsturē |
| `git push` | Nosūta commit uz GitHub (pirmoreiz: `git push -u origin <zars>`) |
| `git fetch origin` | Uzzina, kas jauns GitHub, nemainot tavus failus |
| `git merge origin/main` | Apvieno `main` izmaiņas ar pašreizējo zaru |
| `git log --oneline` | Parāda commit vēsturi |
| `git restore .` | Atmet visas nesaglabātās izmaiņas (**nevar atsaukt**) |

