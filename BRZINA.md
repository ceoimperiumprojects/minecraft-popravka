# 🚀 Minecraft se zaledi / ne može da se mrda — kako da radi brzo

Minecraft se upali, ali kad uđeš u svet **se zaledi** ili je ekstremno spor.
To je zato što je laptop slabiji (stari procesor + 4GB RAM + slabija grafika),
a verzija **1.20.1 je teška**. Idemo da iscedimo maksimum iz njega. 💪

Radimo poteze od najjačeg ka slabijem. Probaj korak 1, pa ako i dalje nije dobro -> korak 2, pa 3.

---

## ⏳ Prvo: ako se zaledi BAŠ kad uđeš u svet

Ne gasi odmah! Stari laptop sa sporim diskom prvih **1-2 minuta** učitava teren
i tad se sve zamrzne. Sačekaj malo - često se odledi sam i posle radi. Ako se NE
odledi za 2 min, idemo na popravke ispod.

---

## 1. Uključi OptiFine (NAJVAŽNIJE — duplira/triplira brzinu)

OptiFine je dodatak koji čini Minecraft mnogo bržim na slabim laptopovima.
TLauncher ga ima **ugrađenog**, ne treba ništa da skidaš ručno:

1. Otvori **TLauncher**
2. Gore gde biraš verziju, klikni na **padajući meni (strelica)**
3. U listi nađi verziju koja u imenu ima **OptiFine** — npr:

```
1.20.1 OptiFine
```

4. Izaberi je i klikni **Install / Igraj**
5. TLauncher će sam da skine OptiFine (treba internet, traje minut)

> Ako se traži Java pri instalaciji OptiFine — imaš je već, samo klikni dalje.

---

## 2. Namesti grafiku na "krompir" režim (u igri)

Kad uđeš u Minecraft:

1. **Options** (Opcije) -> **Video Settings** (Podešavanja grafike)
2. Namesti ovako:

| Podešavanje | Stavi na |
|---|---|
| **Render Distance** (daljina prikaza) | **4** (ili čak 2-3) |
| **Graphics** (grafika) | **Fast** (brzo) |
| **Smooth Lighting** | **OFF** |
| **VSync** | **OFF** |
| **Particles** (čestice) | **Minimal** |
| **Clouds** (oblaci) | **OFF** |
| **Entity Shadows** (senke) | **OFF** |
| **Max Framerate** | **30** ili **60** |

3. Ako ima OptiFine: u **Performance** uključi **Smart/Fast Render** i **Fast Math**.

> Što je manja "Render Distance", to je brže. Na ovom laptopu 4 ili manje je idealno.

---

## 3. Ako i dalje koči — pređi na lakšu verziju (1.12.2)

Verzija **1.20.1 je iskreno preteška** za ovaj laptop. Verzija **1.12.2 radi
kao podmazana** na starim mašinama, a igra je skoro ista.

U TLauncher padajućem meniju izaberi:

```
1.12.2 OptiFine
```

Pa ponovi podešavanja iz koraka 2. Razlika u brzini je OGROMNA. 🔥

---

## 💡 RAM u TLauncheru (prema verziji)

U TLauncher **Settings** -> RAM:

- **1.20.1** -> stavi **2048 MB** (treba mu više)
- **1.12.2** -> **1024-1536 MB** je sasvim dovoljno

> Ne preko 2048 MB — laptop ima ukupno 4GB, mora da ostane i za sistem.

---

### Redosled koji preporučujem:
### 1.12.2 OptiFine + render distance 4 + sve na Fast = **leteće** na ovom laptopu. 🚀
