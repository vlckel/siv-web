# SIV — web

Statický web o jednom souboru. Žádný build, žádné závislosti.

- `index.html` — celý web (HTML + CSS + JS v jednom souboru)

## Publikace na GitHub Pages

Repozitář → **Settings** → **Pages** → Build and deployment →
Source: **Deploy from a branch** → Branch: `main`, složka `/ (root)` → **Save**.

Po minutě běží na `https://<uzivatel>.github.io/<repozitar>/`.
Každý push do `main` se projeví na webu do zhruba minuty.

## Google Kalendář

V `index.html`, na začátku `<script>`:

```js
const CAL = {
  calendarId: "",   // ID veřejného kalendáře
  apiKey:     "",   // API klíč (Google Cloud Console)
  maxResults: 40
};
```

1. Google Kalendář → Nastavení kalendáře → **Přístupová práva**:
   zaškrtnout „Zpřístupnit veřejnosti" (stačí *Zobrazit pouze volné/obsazené*
   NE — je potřeba **Zobrazit všechny podrobnosti události**).
2. Tamtéž níž „Integrovat kalendář" → zkopírovat **ID kalendáře** do `calendarId`.
3. [console.cloud.google.com](https://console.cloud.google.com) → nový projekt →
   APIs & Services → povolit **Google Calendar API** → Credentials →
   Create credentials → **API key** → vložit do `apiKey`.
4. U klíče nastavit **Application restrictions → Websites** a povolit jen
   domény webu (`https://<uzivatel>.github.io/*`, případně `https://www.siv2024.eu/*`),
   a **API restrictions → Google Calendar API**.

Klíč bude v repozitáři veřejně viditelný — proto ta omezení v bodě 4.
Bez nich by ho mohl použít kdokoli a vyčerpat kvótu projektu.

## Vlastní doména (siv2024.eu)

1. Do repozitáře přidat soubor `CNAME` s jediným řádkem: `www.siv2024.eu`
2. U registrátora domény nastavit DNS:
   - `www` → CNAME → `<uzivatel>.github.io`
   - kořen domény (`@`) → A záznamy:
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. Settings → Pages → Custom domain → vyplnit doménu → zaškrtnout **Enforce HTTPS**
   (certifikát se vystaví sám, může to trvat i pár hodin).

Pozor: přesměrováním domény přestane fungovat současný web na Webnode.
Dokud se web netestuje na `github.io` adrese, doménu neměňte.
