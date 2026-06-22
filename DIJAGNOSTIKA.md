# 🔍 Dijagnostika — zašto Minecraft neće da upali

Ako Minecraft **neće da se pokrene** (ne zaledi se, nego prosto neće), prvo treba da
vidimo šta fali. Obično je u pitanju **Java** ili **grafički drajver (OpenGL)**.

> Kao i pre: samo **kopiraj** blok (dugme gore desno u sivom okviru), **nalepi** u
> terminal, Enter. Idi redom. 🙂

---

## 1. Otvori terminal

```
Ctrl + Alt + T
```

---

## 2. Pokreni dijagnostiku

Nalepi ceo ovaj blok odjednom:

```bash
echo "=== JAVA ==="
java -version 2>&1 || echo ">>> JAVA NIJE INSTALIRANA <<<"

echo ""
echo "=== KOJE JAVE POSTOJE ==="
ls /usr/lib/jvm/ 2>/dev/null || echo ">>> nema nijedne Jave <<<"

echo ""
echo "=== GRAFICKA KARTICA ==="
lspci | grep -iE "vga|3d|display" || echo "lspci nema info"

echo ""
echo "=== OPENGL / DRAJVER ==="
glxinfo 2>/dev/null | grep -iE "OpenGL version|OpenGL renderer|direct rendering" || echo ">>> glxinfo nije instaliran (videcemo to u koraku 3) <<<"

echo ""
echo "=== SISTEM ==="
uname -a
```

📸 **Slikaj ceo ekran i pošalji.** Na osnovu toga znamo tačno šta fali.

---

## 3. Ako gore piše da `glxinfo` nije instaliran

Nalepi ovo (instalira alat za proveru grafike), pa ponovi korak 2:

```bash
sudo apt update && sudo apt install -y mesa-utils
```

---

## 4. Ako gore piše ">>> JAVA NIJE INSTALIRANA <<<"

Minecraft 1.20.1 traži **Javu 17**. Nalepi ovo da je instaliraš:

```bash
sudo apt update && sudo apt install -y openjdk-17-jre
```

Posle instalacije proveri:

```bash
java -version
```

Treba da piše nešto kao `openjdk version "17..."`.

---

## 5. Kako da TLauncher koristi pravu Javu

1. Otvori **TLauncher**
2. Idi u **Settings** (podešavanja)
3. Nađi polje za **Java path** / **Putanja do Jave**
4. Klikni **Browse** i izaberi:

```
/usr/lib/jvm/java-17-openjdk-amd64/bin/java
```

> Ako ne vidiš baš taj folder, u koraku 2 ti je `ls /usr/lib/jvm/` ispisao koji
> tačno postoje — pošalji sliku pa ti kažemo koji da izabereš.

---

### Posle ovoga probaj opet Minecraft 1.20.1 vanilla. Ako i dalje neće — slikaj grešku! 💪
