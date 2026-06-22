# 🔌 Povezivanje preko Tailscale — tačne komande (za Elenu)

Cilj: da se Pavle poveže na laptop. Elena pokrene komande **redom**, jednu po jednu.

> Kopiraj blok (dugme gore desno u sivom okviru), nalepi u terminal, Enter.
> Terminal se otvara sa `Ctrl + Alt + T`.

---

### ⚠️ Pre svega — Pavle pošalje ključ
Pavle ide na https://login.tailscale.com/admin/settings/keys -> **Generate auth key**
-> kopira `tskey-auth-...` -> pošalje Eleni. Taj ključ ide u korak 3.

---

## 1. Otvori terminal
```
Ctrl + Alt + T
```

## 2. Instaliraj Tailscale
```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

## 3. Instaliraj SSH (da Pavle može da uđe)
```bash
sudo apt update && sudo apt install -y openssh-server
sudo systemctl enable --now ssh
```
> Password se ne vidi dok kucaš — to je normalno. Ukucaj i Enter.

## 4. Uđi u mrežu (zameni TVOJ-KLJUC ključem od Pavla)
```bash
sudo tailscale up --ssh --authkey tskey-auth-k73s25un2V11CNTRL-vHyB7XJRo9KiPNuCwaKbAK7wHrW86aRUe
```

## 5. Pošalji Pavlu ovo što ispiše
```bash
echo "IME: $(whoami)"
tailscale ip -4
```
📤 Pošalji Pavlu **IME** i **IP adresu** (broj `100.x.x.x`). To je sve!

---

### ✅ Gotovo. Pavle se sad povezuje sam i namešta laptop.
