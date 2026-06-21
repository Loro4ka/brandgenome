# Brand Genome — Impression Scan

Landing page for Brand Genome's Impression Scan product — AI-powered brand impression analysis.

## Project Files

| File | Description |
|------|-------------|
| `index.html` | Main landing page (all CSS inline, no JS dependencies) |
| `logo_site.svg` | Brand logo (SVG) |
| `icon_visual.png` | Visual level icon |
| `icon_semantic.png` | Semantic level icon |
| `icon_audience.png` | Audience level icon |
| `screen_1.png`–`screen_8.png` | Report preview screenshots |
| `screen_a1.png`–`screen_a3.png` | Additional report screenshots |

## GitHub

- **Repo:** https://github.com/Loro4ka/brandgenome
- **Remote:** `git@github.com:Loro4ka/brandgenome.git`
- **Branch:** `main`
- **Local path:** `/Users/larisa/Downloads`

### Push workflow
```bash
cd /Users/larisa/Downloads
git add .
git commit -m "update"
git push origin main
```

## Server

- **Host:** `ssh.aidesk24.work`
- **User:** `mimimi`
- **SSH key:** `~/.ssh/aidesk24` (ed25519)
- **SSH config entry:** `Host aidesk24` (uses cloudflared proxy)

### Connect
```bash
ssh aidesk24
```

### Deployment (Docker + Nginx)

```
Docker Container: brandgenome (nginx:alpine)
Bind: 127.0.0.1:3300 → container:80
Nginx: proxy → 127.0.0.1:3300
Domain: brandgenome.online (via Cloudflare Tunnel)
```

### Deploy/Update
```bash
# 1. Upload files
cd /Users/larisa/Downloads
scp index.html logo_site.svg icon_*.png screen_*.png aidesk24:~/brandgenome/

# 2. Rebuild & restart Docker
ssh aidesk24 "cd ~/brandgenome && docker build -t brandgenome . && docker stop brandgenome && docker rm brandgenome && docker run -d --name brandgenome --restart unless-stopped -p 127.0.0.1:3300:80 brandgenome"
```

### Dockerfile location
```
/home/mimimi/brandgenome/Dockerfile
```

### Nginx config
```
/etc/nginx/sites-available/brandgenome
/etc/nginx/sites-enabled/brandgenome → symlink
```

## Live URL

**https://brandgenome.online**

## Design Notes

- Dark theme (`#0a0a0a` background)
- Accent colors: red (`#e63a1e`), green (`#a8e63a`), orange (`#ff7800`)
- Font: Inter (Google Fonts)
- Russian language
- Scroll fade-in animations (IntersectionObserver)
- Hero section with animated gradient orbs
- Overlapping report cards (vertical stack with rotateX)
- Sticky header with logo + Telegram CTA button

## Telegram Bot

- **Handle:** `@brandgenome_bot`
- **Link:** `https://t.me/brandgenome_bot`
