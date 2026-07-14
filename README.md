# wildcard-redirect

---

# Universal Edge Redirection Boilerplate

A multi-platform configuration repository designed to handle instant domain and wildcard subdomain level redirections (`301 Moved Permanently`).

This project is completely serverless, framework-free, and deployment-ready for **Vercel, Netlify, Nginx, or Caddy**. Platforms will only read the configuration file they natively recognize, ignoring the others.

---

## 📂 Project Structure

```text
├── vercel.json     # Edge redirect rules for Vercel
├── netlify.toml    # Platform settings and rules for Netlify
├── _redirects       # Direct fallback engine syntax for Netlify
├── Caddyfile       # Zero-config SSL redirection block for Caddy
└── nginx.conf      # Enterprise-ready proxy routing server block for Nginx

```

---

## 🛠️ Configuration & Customization

Before deploying, open the configuration files and change the dummy URL (`[https://habibullah.dev](https://habibullah.dev)`) to your actual target destination domain.

### 1. Vercel (`vercel.json`)

Change the value inside the `destination` parameter string:

```json
"destination": "https://your-target-domain.com/$1"

```

### 2. Netlify (`netlify.toml` & `_redirects`)

Change the destination mapping inside your TOML or plain text file:

```toml
to = "https://your-target-domain.com/:splat"

```

### 3. Caddy (`Caddyfile`)

Change the primary endpoint string:

```caddy
redir https://your-target-domain.com{uri} permanent

```

### 4. Nginx (`nginx.conf`)

Update the rewrite redirect path rule parameter:

```nginx
return 301 https://your-target-domain.com$request_uri;

```

---

## 🚀 How to Deploy

### Cloud Platforms (Serverless Edge)

#### **Deploying on Vercel**

1. Push this repository to your GitHub account.
2. Go to the **Vercel Dashboard** and click **Add New > Project**.
3. Import this repository (Vercel will detect it as a framework-less project, which is correct).
4. Click **Deploy**.
5. Go to **Project Settings > Domains** and attach your vanity root domain (e.g., `hz.com`) and wildcard domain (e.g., `*.hz.com`).

#### **Deploying on Netlify**

1. Log into your **Netlify Dashboard** and click **Import from Git**.
2. Connect your GitHub account and select this repository.
3. Leave the build command and publish directory fields completely empty.
4. Click **Deploy Site**.
5. Navigate to **Domain Settings** and add your custom domains/wildcard aliases.

---

### Self-Hosted Infrastructure (Linux VPS / Docker)

#### **Deploying on Caddy**

Move the `Caddyfile` into your production deployment location (usually `/etc/caddy/Caddyfile`) and reload the service daemon manager:

```bash
sudo systemctl reload caddy

```

#### **Deploying on Nginx**

Symlink or copy your `nginx.conf` parameters into your active virtual hosts configuration setup directory (e.g., `/etc/nginx/sites-enabled/redirect.conf`) and reload Nginx:

```bash
sudo nginx -t && sudo systemctl reload nginx

```

---

## 📝 Performance Metrics

* **Execution Layer:** Network Edge (CDN / Global Data Centers)
* **Average Redirect Latency:** ~20ms - 50ms
* **HTTP Status Trigger:** `301 Moved Permanently` (Aggressively cached by modern browser engines for instant subsequent access).
