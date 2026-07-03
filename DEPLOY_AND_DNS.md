# CloudPot landing — deploy & DNS

**Live now:** https://cloudpot-landing.netlify.app (Netlify project `cloudpot-landing`, team BT / `rama-krishna1183`).
**Repo:** https://github.com/ramakrishna1183-gif/cloudpot-landing (branch `main`).
**Custom domain:** cloudpot.nl added in Netlify → Domain management (status: *Pending DNS verification*).

Relationship: CloudPot = parent company; **Beyond Theory Guide** is featured as CloudPot's flagship product and links to https://beyondtheorywhatworks.com.

---

## 1. Point cloudpot.nl — YOUR STEP (at the cloudpot.nl registrar's DNS panel)

Add these records where cloudpot.nl's DNS is managed (the registrar you bought it from):

**Apex (cloudpot.nl):** pick ONE
- Preferred — `ALIAS` / `ANAME` / flattened `CNAME` → `apex-loadbalancer.netlify.com`
- Fallback (if registrar has no ALIAS/ANAME) — `A` record → `75.2.60.5`

**www (www.cloudpot.nl):**
- `CNAME` → `cloudpot-landing.netlify.app`

DNS can take up to ~24h to propagate. Once it resolves, Netlify auto-verifies and provisions a free Let's Encrypt HTTPS certificate — no action needed. (Netlify suggests making `www.cloudpot.nl` the primary for best CDN behaviour; optional — current setup with the apex as primary works fine.)

Tip: if the registrar also offers to delegate DNS to Netlify ("Use Netlify DNS"), that's an alternative that auto-creates the records — but the two A/ALIAS/CNAME records above are all you strictly need.

---

## 2. Updating the site later

Right now the site was published by a manual upload. Two ways to update:

**A. Manual (works today, no extra setup):** edit files locally → re-zip → drag into Netlify → Deploys → drop zone. (Or ask me to redeploy.)

**B. Git CI like btww-landing (recommended, one-time setup — YOUR STEP):**
In Netlify → `cloudpot-landing` → Project configuration → Build & deploy → **Link repository** → GitHub → pick `ramakrishna1183-gif/cloudpot-landing`. This needs one click to authorize the Netlify GitHub App on the new repo. After that, every `git push` to `main` auto-deploys — same as btww-landing/btww-chat. Publish directory is repo root (`netlify.toml` already set).
