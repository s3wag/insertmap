
## Goal:
Identify common misconfigurations in web apps, servers, platforms, and services that may expose sensitive information, weaken protections, or allow unauthorized access.

---

## Web Server / Platform Misconfigurations
- [ ] Check for exposed `.git/`, `.svn/`, `.DS_Store` files
- [ ] Check for `/server-status`, `/server-info`, `/config` endpoints
- [ ] Identify directory listing enabled on web paths
- [ ] Access `/WEB-INF/`, `/app.config`, or `/admin/config.php`
- [ ] Detect misconfigured `.htaccess`, `.htpasswd` leaks
- [ ] Test for server-side debug mode (e.g., Flask `?__debugger__`)
- [ ] Identify verbose error messages in stack traces
- [ ] Check `/robots.txt` and `/sitemap.xml` for sensitive files
- [ ] Look for outdated web frameworks (e.g., JSP, Rails)
- [ ] Identify sensitive endpoints with default credentials

---

## Authentication & Access Misconfigurations
- [ ] Default admin credentials (`admin:admin`, `root:toor`)
- [ ] Unrestricted access to admin panels or dashboards
- [ ] Weak password policies / no 2FA enforced
- [ ] Verbose login errors (e.g., user not found vs. wrong password)
- [ ] No account lockout on repeated failed logins
- [ ] JWT secrets hardcoded or guessable
- [ ] Access internal tools exposed publicly
- [ ] Insecure password reset flows (e.g., predictable tokens)
- [ ] Test accounts left in production
- [ ] Use of insecure identity providers or SSO integrations

---

## Cloud / DevOps / Infrastructure Leaks
- [ ] Publicly accessible AWS S3 buckets or Azure blobs
- [ ] `.env`, `.bash_history`, or `.aws/credentials` accessible
- [ ] CI/CD exposure: Jenkins, GitLab, CircleCI dashboards
- [ ] Open Docker/Kubernetes APIs without auth
- [ ] Terraform/Ansible config files with secrets
- [ ] Misconfigured cloud metadata APIs (`169.254.169.254`)
- [ ] Exposed .pem, .ppk, .crt, or .key files
- [ ] AWS credentials leaked in JavaScript
- [ ] GCP/Azure storage links without access control
- [ ] Backup files like `db_backup.sql`, `config.old.php`, `index~.php`

---

## HTTP Header / SSL / Security Settings
- [ ] Missing `X-Frame-Options` (clickjacking)
- [ ] Missing `Strict-Transport-Security`
- [ ] HTTP instead of HTTPS for login or sensitive pages
- [ ] Weak SSL/TLS versions (e.g., SSLv3, TLS 1.0)
- [ ] Insecure CORS policy (`Access-Control-Allow-Origin: *`)
- [ ] Missing or wildcard `Content-Security-Policy`
- [ ] Missing `X-Content-Type-Options: nosniff`
- [ ] Improper cache control on sensitive data
- [ ] Insecure Referrer-Policy (e.g., `unsafe-url`)
- [ ] Lack of certificate pinning for mobile apps

---

## Application Logic & Deployment Errors
- [ ] Debug mode enabled in production (`debug=true`)
- [ ] Error stack traces exposing function names and file paths
- [ ] Verbose exception messages via API or frontend
- [ ] Environment banners like “Staging”, “Dev”, or “Test” live
- [ ] Hardcoded keys/tokens in source or frontend JS
- [ ] Swagger/OpenAPI docs publicly exposed
- [ ] GraphQL introspection enabled in production
- [ ] Admin APIs deployed under `/v1/internal/`, but not protected
- [ ] Hardcoded feature flags or toggles
- [ ] Exposed monitoring interfaces (Grafana, Prometheus)

---
