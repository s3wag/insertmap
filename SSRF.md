
## 🔍 Check these locations where the server may initiate HTTP/HTTPS requests on behalf of the user

---

## 🌐 URL-based Parameters
- [ ] url= 
- [ ] target= 
- [ ] dest= 
- [ ] redirect= 
- [ ] link= 
- [ ] next= 
- [ ] data= 
- [ ] load= 
- [ ] path= 
- [ ] img_url=

---

## Image & File Fetching Features
- [ ] Image preview generators
- [ ] PDF converters (URL input)
- [ ] URL-to-PDF tools
- [ ] Image resizing APIs
- [ ] Website screenshot utilities
- [ ] Link unfurlers (e.g., chat or forums)
- [ ] Thumbnail generation services
- [ ] Image proxy endpoints
- [ ] Media proxy (audio/video)
- [ ] Favicon fetchers

---

## Importers & Fetchers
- [ ] RSS/Atom feed parsers
- [ ] Webhook receivers/testers
- [ ] Social media or profile picture importers
- [ ] Metadata fetchers
- [ ] Content scraping endpoints
- [ ] API integrations with third-party services
- [ ] SSO/OpenID metadata fetch URLs
- [ ] Mail clients fetching remote images
- [ ] URL scanners or validators
- [ ] CI/CD webhooks using URLs

---

## URL Callbacks and Webhooks
- [ ] Webhook listener or tester (`/webhook/test`)
- [ ] OAuth redirect_uri checks (server-side)
- [ ] SAML metadata URL import
- [ ] Callback URLs in integrations
- [ ] CI/CD Git webhook URLs
- [ ] Slack/Teams webhook setup
- [ ] Payment gateway URL callbacks
- [ ] Pingbacks/trackbacks (WordPress/Blog)
- [ ] URL validators in cloud functions
- [ ] API gateway proxy routes

---

## File & Data Processing
- [ ] XML/XSLT with remote DTD or entities (XXE ➜ SSRF)
- [ ] YAML parsers importing external schemas
- [ ] Log shipping endpoints (e.g., `url: syslog://127.0.0.1`)
- [ ] Zip file upload with remote references
- [ ] Export-to-URL functionality
- [ ] Internal file inclusion from user input
- [ ] API that loads config from user-supplied URL
- [ ] File readers that pull files from URLs
- [ ] Archive extractors with URL-based fetches
- [ ] SSRF via DNS rebinding or `Host:` header injection

---

## Bonus: High-Risk Targets (for SSRF payloads)
- [ ] http://169.254.169.254/ (AWS metadata)
- [ ] http://localhost/
- [ ] http://127.0.0.1/
- [ ] http://[::1]/ (IPv6 loopback)
- [ ] Internal admin panels (http://internal/admin)
- [ ] Docker socket (http://localhost:2375/)
- [ ] Kubernetes API (http://127.0.0.1:8001/)
- [ ] Redis (gopher://localhost:6379/_...)
- [ ] FTP or file:// handlers
- [ ] Custom internal services (e.g., http://vault/, http://grafana/)

---

## Tips for Testing SSRF
- [ ] Use Burp Collaborator to detect blind SSRF
- [ ] Try `http`, `https`, `gopher`, `file`, `dict`, `ftp`, and `ldap`
- [ ] Use DNS-based payloads (`http://yourdomain.burpcollaborator.net`)
- [ ] Try encoding (hex, URL-encoded, base64)
- [ ] Bypass filters using `@`, `#`, port smuggling, DNS rebinding

---

