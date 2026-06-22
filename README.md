# 🎮 Minecraft popravka — uputstvo korak po korak

Ovo je uputstvo za laptop koji **zabode (zaledi se)** kad se uđe u Minecraft.
Laptop ima samo 4GB RAM-a, pa ćemo da dodamo **swap** (kao "pomoćnu memoriju" na disku).

> ⚠️ **VAŽNO:** Nemoj da improvizuješ i menjaš komande. Samo **kopiraj** blok po blok
> (klikni dugme za kopiranje gore desno u svakom sivom okviru) i **nalepi** u terminal.
> Idi redom, jedan po jedan blok. 🙂

---

## 1. Otvori terminal

Pritisni na tastaturi istovremeno:

```
Ctrl + Alt + T
```

---

## 2. Ukucaj password jednom

Iskopiraj i nalepi ovo, pa Enter:

```bash
sudo -v
```

Tražiće password. **Dok kucaš password neće se videti NIŠTA** — ni zvezdice, ni tačkice.
To je normalno, tako Linux radi. Samo ukucaj password i pritisni **Enter**.

---

## 3. Proveri stanje PRE (disk, RAM, swap)

Nalepi ceo ovaj blok:

```bash
echo "=== DISK ==="
df -h /

echo "=== RAM I SWAP PRE ==="
free -h
swapon --show
```

📸 **Slikaj ekran i pošalji sliku** pre nego što ideš dalje.

---

## 4. Napravi swap od 8GB

Nalepi ceo ovaj blok odjednom:

```bash
sudo swapoff /swapfile8g 2>/dev/null || true
sudo rm -f /swapfile8g

sudo fallocate -l 8G /swapfile8g || sudo dd if=/dev/zero of=/swapfile8g bs=1M count=8192 status=progress

sudo chmod 600 /swapfile8g
sudo mkswap /swapfile8g
sudo swapon /swapfile8g

grep -q '^/swapfile8g ' /etc/fstab || echo '/swapfile8g none swap sw 0 0' | sudo tee -a /etc/fstab

echo 'vm.swappiness=20' | sudo tee /etc/sysctl.d/99-swappiness.conf
sudo sysctl -p /etc/sysctl.d/99-swappiness.conf

echo "=== RAM I SWAP POSLE ==="
free -h
swapon --show
```

---

## 5. Restartuj laptop

```bash
sudo reboot
```

---

## 6. Posle restarta — proveri da li je swap tu

Otvori opet terminal (`Ctrl + Alt + T`) i nalepi:

```bash
free -h
swapon --show
```

Treba da vidiš negde red sličan ovome:

```
/swapfile8g   8G
```

Ako vidiš `8G` pored `/swapfile8g` — **uspeli smo!** ✅

---

## 7. Test Minecraft-a

1. **Zatvori browser** (Chrome/Firefox) — da ne troši RAM.
2. Otvori **samo TLauncher**.
3. U TLauncher **Settings** (podešavanja) stavi RAM na:

```
1024 MB
```

> Za prvi test neka bude **1024 MB**, ne više.

4. Pokreni **Minecraft 1.20.1 vanilla** (običan, bez modova) prvo.

---

## 8. Ako prvi test prođe dobro

Možeš da podigneš RAM u TLauncher settings na:

```
1536 MB
```

> ❌ **NEMOJ** da staviš 3GB ili 4GB. Laptop ima ukupno 4GB —
> nije NASA kompjuter, nego mali borac koji daje sve od sebe. 😅

---

### To je to! Ako negde zapne, slikaj ekran i pošalji. 💪
