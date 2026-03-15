# Athish Vikraman — 3D Portfolio Website

## Stack
- **Three.js r128** — 3D hero scene (wireframe icosahedron, particle field, orbital rings)
- **Vanilla HTML/CSS/JS** — zero build step, zero dependencies to install
- **Google Fonts** — Instrument Serif + Outfit + IBM Plex Mono
- **Formspree** — contact form backend (already configured)

## Project Structure
```
portfolio3d/
├── index.html      ← Complete website (single file)
├── README.md       ← This file
├── netlify.toml    ← Netlify deploy config
└── assets/
    └── resume.pdf  ← Place your resume here
```

## Local Preview
```bash
# Option 1: Python
cd portfolio3d
python3 -m http.server 8000
# Open http://localhost:8000

# Option 2: Node
npx serve .
```

## Deployment

### GitHub Pages (Free)
```bash
# 1. Create repo named: athishvikraman.github.io
git init
git add .
git commit -m "Deploy portfolio"
git remote add origin git@github.com:YOUR_USERNAME/athishvikraman.github.io.git
git push -u origin main

# 2. Go to repo Settings → Pages → Source: main branch, root
# 3. Live at: https://athishvikraman.github.io
```

### Netlify (Free, recommended for custom domain)
```bash
# 1. Push to any GitHub repo
# 2. Go to netlify.com → New Site → Import from Git
# 3. Publish directory: . (root)
# 4. Click Deploy
# 5. Live in 30 seconds with free HTTPS
```

### Vercel (Free)
```bash
# 1. Push to GitHub
# 2. Go to vercel.com → Import Project
# 3. Framework: Other
# 4. Root directory: . (default)
# 5. Deploy
```

## Custom Domain Setup

### On Netlify:
1. Go to Site Settings → Domain Management → Add custom domain
2. Enter: `athishvikraman.com` (or your domain)
3. Netlify gives you a DNS target (e.g., `your-site.netlify.app`)
4. At your domain registrar (GoDaddy, Namecheap, Cloudflare, etc.):
   - Add **CNAME** record: `www` → `your-site.netlify.app`
   - Add **A** record: `@` → `75.2.60.5` (Netlify's load balancer)
5. Enable HTTPS in Netlify (automatic with Let's Encrypt)
6. Wait 5–30 minutes for DNS propagation

### On Vercel:
1. Go to Project Settings → Domains → Add
2. Enter your domain
3. Vercel gives you DNS records to add at your registrar
4. HTTPS is automatic

### On GitHub Pages:
1. Go to repo Settings → Pages → Custom domain
2. Enter your domain
3. Add these DNS records at your registrar:
   - **A** records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - **CNAME** (for www): `YOUR_USERNAME.github.io`
4. Check "Enforce HTTPS"

## Where to Edit Content

### Personal Links (search and replace)
| Item | Find in code | Replace with |
|------|-------------|--------------|
| Resume | `href="#"` on "Resume" button | `href="assets/resume.pdf"` |
| GitHub | `https://github.com/` | Your GitHub URL |
| LinkedIn | `https://linkedin.com/in/` | Your LinkedIn URL |
| Email | `athishvikraman22@gmail.com` | Already set |
| Formspree | `mlgpdgnb` | Already set |

### Projects
Each project is a `<div class="pcard">`. To add new ones:
```html
<div class="pcard rv" data-cat="grad">
  <div class="ptype">Graduate · Course</div>
  <h3>Title</h3>
  <p class="pdesc">Description.</p>
  <div class="ptech"><span>Tech</span></div>
  <div class="plinks"><a href="URL">GitHub →</a></div>
</div>
```
Set `data-cat` to `"grad"` or `"ug"` for filter tabs.

### 3D Scene Customization
The Three.js scene is at the bottom of `index.html` inside a `<script>` block.
- Change accent color: replace `0x0d9488` (hex without #)
- Particle count: change `pCount = 300`
- Geometry size: change `IcosahedronGeometry(1.8, 1)` first param
- Camera distance: change `camera.position.z = 4.5`

### Color Theme
Edit CSS variables at the top of `<style>`:
```css
--accent: #0d9488;          /* Main teal */
--accent-bright: #2dd4bf;   /* Light teal */
--gold: #e2b94a;            /* Featured highlight */
--bg-void: #060a12;         /* Darkest background */
```

## Performance Notes
- Three.js renders at device pixel ratio capped at 2x (saves GPU on high-DPI)
- Particles: 300 count (light on GPU)
- All animations are CSS-based except the 3D hero (requestAnimationFrame)
- Intersection Observer for lazy scroll reveals (no scroll event spam)
- Single HTTP request for the entire site (just index.html + fonts + Three.js CDN)
