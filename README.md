# Athish Vikraman — Portfolio Website
 
## Stack
- **Three.js r128** — 3D hero scene (wireframe dodecahedron, particle field, orbital rings, gold accent)
- **Vanilla HTML/CSS/JS** — zero build step, zero dependencies
- **Google Fonts** — Fraunces + Manrope + JetBrains Mono
- **Formspree** — contact form backend (configured at `mlgpdgnb`)
 
## Project Structure
```
portfolio/
├── index.html      ← Complete website (single file)
└── README.md       ← This file
```
 
> All report PDFs are hosted on Google Drive and linked directly in `index.html`. No local PDF files are needed.
 
## Local Preview
```bash
# Option 1: Python
python3 -m http.server 8000
# Open http://localhost:8000
 
# Option 2: Node
npx serve .
```
 
> Must run via a local server — opening `index.html` directly via `file://` will block Three.js from loading.
 
## Deployment
 
### GitHub Pages (current setup)
```bash
# 1. Create repo (e.g. portfolio or athishvikraman.github.io)
git init
git add .
git commit -m "Deploy portfolio"
git remote add origin git@github.com:athish22072003/portfolio.git
git push -u origin main
 
# 2. Repo → Settings → Pages → Source: main branch, root
# 3. Live at: https://athish22072003.github.io/portfolio/
```
 
### Netlify (recommended for custom domain)
```bash
# 1. Push to GitHub
# 2. netlify.com → New Site → Import from Git
# 3. Publish directory: . (root)
# 4. Deploy — live in ~30 seconds with free HTTPS
```
 
## Custom Domain Setup
 
### On Netlify:
1. Site Settings → Domain Management → Add custom domain
2. Add **CNAME**: `www` → `your-site.netlify.app`
3. Add **A** record: `@` → `75.2.60.5`
4. Enable HTTPS (automatic via Let's Encrypt)
 
### On GitHub Pages:
1. Repo Settings → Pages → Custom domain
2. Add these **A** records at your registrar:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
3. Add **CNAME** (for www): `athish22072003.github.io`
4. Check "Enforce HTTPS"
 
## Content Map
 
### Personal Links
| Item | Location in code | Current value |
|------|-----------------|---------------|
| Email | Contact section `mailto:` | `athishvikraman22@gmail.com` |
| LinkedIn | Hero button + Contact section | `linkedin.com/in/athishvikraman` |
| GitHub | Contact section | `github.com/athish22072003` |
| RV32 Repo | Featured project card | `github.com/athish22072003/rv32im-systolic-coprocessor` |
| Formspree | Contact form `action=` | `https://formspree.io/f/mlgpdgnb` |
 
### Report Links (Google Drive)
All PDFs are linked via Google Drive share URLs. To update a link, find the card by its `<h3>` title and replace the `href` in its `<div class="plinks">`.
 
| Card | File |
|------|------|
| Parameterized Pipelined Datapath (Lab 1) | `FPGA_Lab_1.pdf` |
| Dot-Product Accelerator (Lab 2) | `Lab2_Report_Final.pdf` |
| Warehouse Surveillance System | `ECSE488_Midterm_FINAL.pdf` |
| HfO₂ Ferroelectric Devices | `Final_Project_Proposal.pdf` |
| 1D P-N Junction Simulation | `ECSE422_modelling_report_1.pdf` |
| 2D P-I-N Junction Light Response | `ECSE422_Modeling_Report_2_final.pdf` |
 
### Adding a New Project Card
```html
<div class="pc gc rv">
  <div class="pl">COURSE · Tool · Type</div>
  <h3>Project Title</h3>
  <p class="pd">Description.</p>
  <div class="pr"><strong>Results:</strong> Key numbers here.</div>
  <div class="pt"><span>Tech</span><span>Tool</span></div>
  <div class="plinks">
    <a href="GOOGLE_DRIVE_LINK" target="_blank">Report →</a>
    <a href="GITHUB_LINK" target="_blank" class="gh">⬡ GitHub →</a>
  </div>
</div>
```
Use `gc` for graduate projects, `uc` for undergraduate.
 
### 3D Scene (Hero)
The Three.js scene is at the bottom of `index.html` inside the main `<script>` block.
- **Accent color**: replace `0xd4af37` (royal gold)
- **Particle count**: change `N=250`
- **Main geometry**: `DodecahedronGeometry(2.4, 0)`
- **Camera start distance**: `cam.position.set(0, 0, 12)`
 
### Color Theme
```css
--teal: #d4af37;        /* Royal gold — primary accent */
--teal-lt: #fceda6;     /* Light gold — highlights */
--gold-dim: #a68c4a;    /* Muted gold — gradients */
--purp: #8a1c1c;        /* Royal crimson — undergrad tags */
--void: #050505;        /* Deepest background */
```
 
## Known Issues
- **Cloudflare email obfuscation**: If you view `index.html` through a Cloudflare-proxied URL, the email link will be replaced with `/cdn-cgi/l/email-protection#...`. This does not happen on GitHub Pages or Netlify. The raw `index.html` file always contains the correct `mailto:athishvikraman22@gmail.com`.
- **PDF links**: All PDFs link to Google Drive. If a Drive link expires or file access is revoked, update the `href` in the relevant project card's `<div class="plinks">`.
