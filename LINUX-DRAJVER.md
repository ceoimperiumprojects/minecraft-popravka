# 🎯 Štuca na Mint-u, a radilo na Windows 7 — to je DRAJVER

Ako je **ista verzija sa istim modovima radila na Windows 7** na ovom istom laptopu,
ali na Linux Mint-u štuca/zapucava — onda **nije** ni mod, ni RAM, ni verzija.

Problem je da Minecraft na Mint-u verovatno renderuje preko **procesora**
(tzv. `llvmpipe` = software rendering) umesto preko **grafičke kartice**.
To ubija FPS. Idemo da proverimo i popravimo.

> Kopiraj blok (dugme gore desno), nalepi u terminal (`Ctrl+Alt+T`), Enter.

---

## 1. PROVERA — da li koristi grafičku ili procesor?

Nalepi ovo:

```bash
sudo apt update && sudo apt install -y mesa-utils

echo ""
echo "=== OPENGL RENDERER (NAJVAZNIJE) ==="
glxinfo | grep -iE "OpenGL renderer|OpenGL version|direct rendering"

echo ""
echo "=== CPU GOVERNOR ==="
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor 2>/dev/null | sort -u

echo ""
echo "=== KOJA GRAFICKA ==="
grep -m1 "model name" /proc/cpuinfo
lspci | grep -iE "vga|3d|display"
```

📸 **Slikaj i pošalji.** Gledamo red `OpenGL renderer:`

- Ako piše ime grafičke (npr. `Mesa Intel...`, `AMD...`) -> dobro, grafička radi
- Ako piše **`llvmpipe`** ili **`softpipe`** -> ❌ renderuje preko procesora, TO je problem

---

## 2. POPRAVKA — instaliraj prave Intel/Mesa drajvere

Nalepi (popravlja najčešći uzrok):

```bash
sudo apt update
sudo apt install -y libgl1-mesa-dri mesa-vulkan-drivers libglx-mesa0 xserver-xorg-video-intel
```

Pa **restartuj**:

```bash
sudo reboot
```

Posle restarta ponovi PROVERU iz koraka 1 — `OpenGL renderer` više ne sme da bude `llvmpipe`.

---

## 3. POPRAVKA — natera procesor da radi punom brzinom

Na Linuxu stari laptopi često drže procesor na "štednji" (powersave) pa štuca.
Nalepi da ga prebaciš na **performance**:

```bash
sudo apt install -y cpufrequtils
echo 'GOVERNOR="performance"' | sudo tee /etc/default/cpufrequtils
sudo systemctl restart cpufrequtils 2>/dev/null
sudo cpufreq-set -r -g performance 2>/dev/null

echo "=== PROVERA (treba da pise performance) ==="
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_governor 2>/dev/null | sort -u
```

---

## 4. Sitnica koja mnogo pomaže — isključi efekte radne površine

Minty (Cinnamon) "compositor" usporava igre. U igri igraj u **Windowed** modu
(prozor), ili probaj fullscreen — vidi šta je glađe.

Takođe: zatvori SVE ostalo (browser, programe) dok igraš.

---

### Najverovatniji krivac: `llvmpipe` u koraku 1. Ako to vidimo -> korak 2 to rešava. 💪
