# BK LAS 2026 — Research Hub

> SupremeLeader's intel bunker for EU funding in Bela Krajina. Static, unbreakable, no nonsense.

A static HTML research hub mapping EU funding opportunities for sustainable projects in the Kolpa river region, Bela Krajina, Slovenia. Built to empower farmers, NGOs, and municipalities with actionable grant data — biodiversity, eco-tourism, green agriculture, youth entrepreneurship.

## What This Is

Pure static HTML/CSS. No build tools, no npm, no JS frameworks. Every file is self-contained with embedded styles. Load and go. Data is baked in from real-time xbridge research sessions — frozen in HTML, accurate as of 15.3.2026.

**Live URL:** https://hrco.github.io/bk-las-2026/
**Repo:** github.com/hrco/bk-las-2026 (public)

## File Structure

```
BK-las-2026/
├── index.html                              ← Dashboard + deadline calendar
├── 01-kolpa-biodiversity-citizen-science.html  ← EKSRP €80k
├── 02-kolpa-farm-trail-markets.html            ← ESRR €120k
├── 03-perma-kolpa-gardens.html                 ← EKSRP €200k
├── 04-kolpa-floating-hubs.html                 ← ESRR €250k
├── 05-kolpa-youth-venture-lab.html             ← ESRR €40k
├── 06-kolpa-inclusive-access.html              ← EKSRP €100k
├── 07-kolpa-night-sky-gastro.html              ← ESRR €90k
├── guide-erasmus-ka220.html                    ← ⚡ Deadline 26.3.2026
├── guide-interreg-sihr.html                    ← Deadline 15.6.2026
├── guide-life-nature.html                      ← Deadline 23.4.2026
├── guide-arsktrp-p41.html                      ← Deadline ~30.4.2026
├── guide-eit-food.html                         ← Deadline ~30.4.2026
├── guide-spirit-rural.html                     ← Deadline 15.5.2026
├── guide-las-dbk-prep.html                     ← LAS DBK prep (no open call)
└── CLAUDE.md
```

## Serving Locally

```bash
cd /home/supremeleader/mylab/BK-las-2026
python3 -m http.server 8765
# → http://localhost:8765
# → http://100.78.95.58:8765  (Tailscale)
```

## Publishing

GitHub Pages — auto-deploys on push to `main`:

```bash
git add .
git commit -m "feat: update funding deadlines"
git push
# live in ~60 seconds at hrco.github.io/bk-las-2026
```

## Local Tunnel (no sudo)

For sharing previews without full deploy:

```bash
# Cloudflare (already installed, no account needed)
nohup cloudflared tunnel --url http://localhost:8765 > /tmp/cf-bk.log 2>&1 &
grep -o 'https://[a-z0-9-]*\.trycloudflare\.com' /tmp/cf-bk.log | tail -1

# Get URL after restart
grep -o 'https://[a-z0-9-]*\.trycloudflare\.com' /tmp/cf-bk.log | tail -1
```

User systemd services exist for auto-start on login:
```bash
systemctl --user status bk-las-server.service
systemctl --user status bk-las-tunnel.service
```

Tailscale Funnel (stable URL, needs operator set once):
```bash
sudo tailscale set --operator=$USER  # one-time
tailscale funnel --bg 8765
```

## xbridge MCP Tools

How we built this — Grok via xbridge for all research. Use these to update content when calls open.

| Tool | When to use |
|------|------------|
| `grok-chat` | Quick one-off fact-checks — verify a single deadline, check a funding amount |
| `grok-session-create` + `grok-session-chat` | Multi-turn research sessions — iterative deep dives like our full BK brainstorm (session: `aefd7c2e`) |
| `grok-web-search` | Real-time EU funding deadlines and open calls — run before updating guide pages |
| `grok-x-search` | Scan X for what Slovenian NGOs and farmers are saying about EU rural programs — adds ground truth |
| `grok-chain-research` | Complex multi-step funding landscape analysis — e.g., map LAS DBK overlaps with Interreg, LIFE, SPIRIT |
| `grok-image-generate` | Visual assets — stylized Kolpa maps, project infographics, header images (not used yet) |

**Example workflow for updating a guide page:**

```
1. grok-web-search: "Interreg VI-A SI-HR 2026 open calls deadline"
2. grok-chat: "Summarize eligibility for LAG applicants in Bela Krajina"
3. Update guide-interreg-sihr.html manually
4. git push
```

**Active sessions:**
- `aefd7c2e-01e0-4d32-bc85-c5acfcdac30d` — LAS Bela Krajina 2026 research session

## Commit Style

```
feat: add night sky IDA certification section
fix: correct Erasmus+ deadline (26.3, not 30.3)
docs: update CLAUDE.md with tunnel instructions
chore: refresh LAS DBK status banners
```

One logical change per commit. Push after every meaningful update.

## Content Rules

- **Language:** Always Slovenian. Proper diacritics (Bela krajina, ne Bela Krajina).
- **Data-driven:** Every fact needs a source. Cite inline with links.
- **Cite sources:** Footer per page with `Vir: las-dbk.si`, `Vir: interreg.si-hr.eu`, etc.
- **No fluff:** Deadlines, amounts, eligibility, steps. That's it.
- **Update cycle:** Re-run `grok-web-search` on open calls before each LAS DBK deadline window.
- **No JS:** Keep pages self-contained. If it needs JavaScript, rethink it.

## Key Contacts (baked into guides)

| Entity | Contact |
|--------|---------|
| LAS DBK | las@ra-dc.si · 07 337 42 23 · las-dbk.si |
| CMEPIUS (Erasmus+) | info@cmepius.si · +386 1 430 47 47 |
| Interreg SI-HR JS | info@si-hr.eu · jems.si-hr.eu |
| LIFE NCP Slovenia | matjaz.mastnak@gov.si |
| ARSKTRP | aktrp@gov.si · 01 580 77 92 |
| SPIRIT Slovenia | spirit@spirit.si · 01 5898 550 |

---

*Built by SupremeLeader + SpectreHawk. Research by Grok via xbridge. Deployed on GitHub Pages.*
*The Kolpa remembers. Go get the funding.*
