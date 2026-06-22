# 🆘 EMERGENCY — daljinski pristup (Pavle ulazi i namešta sam)

Ako ništa drugo ne upali, Pavle će da uđe na laptop **preko Tailscale-a** (sigurna
privatna mreža) i namesti sve sam. Elena treba da pokrene samo **2 komande jednom**.

> Kopiraj blok, nalepi u terminal (`Ctrl+Alt+T`), Enter.

---

## ⚠️ Pavle prvo (sa svog laptopa)

Napravi jednokratni auth ključ da Elenin laptop uđe u tvoj tailnet bez tvog logina:

1. Otvori: https://login.tailscale.com/admin/settings/keys
2. **Generate auth key** -> (opciono Reusable off) -> kopiraj ključ `tskey-auth-...`
3. Pošalji taj ključ Eleni (ide u komandu ispod)

---

## Elena — 1. Instaliraj Tailscale

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

## Elena — 2. Uđi u mrežu + otvori SSH

Zameni `TVOJ-KLJUC-OVDE` ključem koji ti je Pavle poslao:

```bash
sudo apt update && sudo apt install -y openssh-server
sudo systemctl enable --now ssh
sudo tailscale up --ssh --authkey TVOJ-KLJUC-OVDE
```

Na kraju nalepi ovo i **pošalji Pavlu šta ispiše** (to je adresa laptopa):

```bash
echo "KORISNICKO IME: $(whoami)"
tailscale ip -4
```

✅ To je sve sa Eleninog laptopa. Sad Pavle preuzima.

---

## Pavle — ulazak

Sa svog laptopa (zameni IP i ime koje ti je Elena poslala):

```bash
ssh ELENINO-IME@100.x.x.x
```

Ako pita za password — to je Elenin password od laptopa.

Provera da je živa veza:

```bash
tailscale status | grep -i elena
```

---

### Napomena
SSH ti daje terminal — dovoljno za drajvere, governor, mesa, podešavanja.
Za GUI (da vidiš ekran / TLauncher) kasnije možemo VNC, ali 90% popravki je terminal.
