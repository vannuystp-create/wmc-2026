# WMC 2026 · Deployment Checklist
*Symbiotic Spark BV · Tom Vannuys & Ralph Lempers*

---

## Wat je hebt — de drie bestanden

```
index_wmc.html        →  hernoem naar  index.html
wmc_dashboard.html    →  hernoem naar  dashboard.html
vercel.json           →  vervangt de bestaande vercel.json
```

De TypeScript-bestanden (wmc-fixes.zip, wmc-module-content.zip) zijn
architectuurmateriaal voor het post-WMC Next.js platform. **Niet nodig nu.**

---

## Stap 1 — Supabase (5 minuten, één keer)

1. Open **Supabase Dashboard** → jouw project → **SQL Editor** → **New query**
2. Open `wmc_supabase_setup.sql`
3. Kopieer alles → plak → klik **RUN**
4. Verwacht resultaat onderaan: 5 rijen met tabelnamen en kolomaantallen

Dat is het. Drie tabellen aangemaakt, Koraal-data niet aangeraakt.

> De app werkt ook zonder Supabase (localStorage-modus).
> Supabase voegt toe: sergeant-dashboard ziet live data,
> badge-voortgang synct tussen apparaten.

---

## Stap 2 — Vercel (10 minuten, eenmalig)

### Optie A — nieuw WMC-project (aanbevolen)

```bash
# In je lokale map met de drie bestanden:
vercel --name wmc-2026
```

Of via Vercel Dashboard:
1. **New Project** → import uit GitHub of upload folder
2. **Framework Preset**: Other
3. **Environment Variables** → voeg toe:
   ```
   ANTHROPIC_API_KEY = sk-ant-...
   ```
4. Deploy → klaar

### Optie B — zelfde project als Koraal

Vervang `index.html` en `dashboard.html` in het bestaande Vercel-project.
Voeg de WMC-routes toe aan `vercel.json` (al gedaan in de nieuwe versie).

> **Aanbeveling**: apart project. URL: `wmc.symbioticspark.nl`
> Dan kan Koraal ongestoord doordraaien.

---

## Stap 3 — Domein koppelen (5 minuten)

In Vercel → Project → Settings → Domains:
```
wmc.symbioticspark.nl
```
DNS bij jouw registrar: CNAME → `cname.vercel-dns.com`

SSL wordt automatisch aangemaakt door Vercel.

---

## Stap 4 — Testen (voor go-live)

Gebruik deze tokens voor de test:

| Token | Rol | Test |
|-------|-----|------|
| `WMC26-TOM-CEO-2X9P` | Manager | Volledige toegang |
| `WMC26-RALPH-COO-8K4M` | Manager | Volledige toegang |
| `WMC26-SGT-ROD-A1B2` | Sergeant Rodahal | Sergeant-view |
| `WMC26-V001-ROD-M4N5` | Vrijwilliger | Onboarding → Academie |

**Testpad vrijwilliger:**
```
wmc.symbioticspark.nl?token=WMC26-V001-ROD-M4N5
```
Verwacht: WMC-onboarding (4 stappen) → home met countdown + check-in + badges
→ 🎓 Academie tab → Module 1 De Hartslag

**Testpad sergeant:**
```
wmc.symbioticspark.nl/dashboard
```
(Inloggen met sergeant-token in de main app eerst voor sessie)

---

## Nog te doen na deployment

| Item | Wanneer | Hoe |
|------|---------|-----|
| Vrijwilligers uitnodigen | 3–4 weken voor WMC | Genereer uitnodigingslinks met token in URL |
| QR shift-verificatie | Bouwen vóór go-live | Volgende bouwblok |
| WMC officieel logo SVG | Zodra media kit binnen is | 1 SVG vervangen, 10 minuten |
| BV formeel oprichten | Zo snel mogelijk | Notaris John Diederen · Metis Notarissen |

---

## Supabase SQL — samenvatting tabellen

| Tabel | Doel | Koraal-data |
|-------|------|-------------|
| `wmc_profiles` | Onboarding sync | ✗ Niet aangeraakt |
| `badge_progress` | Badge voortgang | ✗ Nieuw |
| `wmc_checkins` | Anonieme check-ins | ✗ Nieuw |
| `profiles` | Koraal profielen | ✓ Blijft intact |
| `pi_measurements` | Koraal PI-data | ✓ Blijft intact |

---

*Versie: 30 april 2026 · Symbiotic Spark BV*
