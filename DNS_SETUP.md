# DNS Configuration for khujaev.com Subdomains

## Current Setup
The repository is configured for GitHub Pages with path-based routing:
- `khujaev.com` → Main landing page
- `khujaev.com/temur/` → Temur's portfolio
- `khujaev.com/dilshod/` → Dilshod's portfolio

## To Configure True Subdomains

### Option 1: Using GitHub Pages (Recommended)
GitHub Pages doesn't support multiple subdomains pointing to the same repository. You'll need separate repositories:

1. **Create separate repositories:**
   - `temur-khujaev` or `temur.khujaev.com` repository
   - `dilshod-khujaev` or `dilshod.khujaev.com` repository

2. **Move content to respective repos:**
   - Copy `temur/index.html` to the root of temur's repo
   - Copy `dilshod/index.html` to the root of dilshod's repo

3. **Add CNAME files:**
   - In temur's repo: Create CNAME file with `temur.khujaev.com`
   - In dilshod's repo: Create CNAME file with `dilshod.khujaev.com`

4. **Configure DNS records at your domain registrar:**
   ```
   Type    Name       Value
   ------  ---------  ---------------------------
   CNAME   temur      [username].github.io.
   CNAME   dilshod    [username].github.io.
   CNAME   www        [username].github.io.
   A       @          185.199.108.153
   A       @          185.199.109.153
   A       @          185.199.110.153
   A       @          185.199.111.153
   ```

### Option 2: Using a Different Hosting Service
If you want to keep everything in one repository with true subdomains, consider:

1. **Netlify** (Free tier available)
   - Supports subdomain redirects
   - Can deploy from a single GitHub repo
   - Configure redirects in `_redirects` file

2. **Vercel** (Free tier available)
   - Supports multiple domains/subdomains
   - Easy GitHub integration
   - Configure in `vercel.json`

3. **CloudFlare Pages** (Free tier available)
   - Excellent subdomain support
   - Built-in CDN
   - Configure via dashboard

## Current Path-Based Solution (Already Implemented)
The current setup works well for:
- Single repository management
- Easy updates and maintenance
- SEO-friendly URLs
- No additional DNS configuration needed

Users can access:
- Main page: `https://khujaev.com`
- Temur's portfolio: `https://khujaev.com/temur/`
- Dilshod's portfolio: `https://khujaev.com/dilshod/`

## DNS Records for Current Setup
For the current GitHub Pages setup, you only need:

```
Type    Name    Value
------  ------  ---------------------------
CNAME   www     [username].github.io.
A       @       185.199.108.153
A       @       185.199.109.153
A       @       185.199.110.153
A       @       185.199.111.153
```

These are GitHub Pages' IP addresses. The CNAME file in the repository handles the custom domain.

## Verification Steps
1. After updating DNS records, wait 24-48 hours for propagation
2. Use `dig` or `nslookup` to verify:
   ```bash
   dig khujaev.com
   dig temur.khujaev.com
   dig dilshod.khujaev.com
   ```
3. Check GitHub Pages settings in repository settings
4. Ensure HTTPS is enabled after DNS propagation

## Important Notes
- DNS changes can take up to 48 hours to propagate globally
- Always use trailing dots in CNAME values (e.g., `username.github.io.`)
- GitHub Pages automatically handles SSL certificates via Let's Encrypt
- The current path-based approach is simpler and requires no additional configuration