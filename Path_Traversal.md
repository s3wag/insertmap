
---

## URL & Route-Based Entry Points (1–10)
- [ ] Direct file access (`/download?file=report.pdf`)
- [ ] Image fetcher endpoint (`/fetch?img=cat.jpg`)
- [ ] Document previewer (`/preview?doc=invoice.docx`)
- [ ] Static resource loader (`/static?path=css/style.css`)
- [ ] Path-based file renderers (`/render/path/to/file`)
- [ ] Template preview/loaders (`/template?name=default`)
- [ ] Log viewer endpoints (`/logs?file=app.log`)
- [ ] Config file loader (`/config?load=default.conf`)
- [ ] Import/export endpoints (`/import?path=file.csv`)
- [ ] Report generation or archival fetcher (`/report?path=/archives/q1.zip`)

---

## User Input Fields Referencing Files
- [ ] Avatar/image upload field (stored path used later)
- [ ] Resume/CV upload download link
- [ ] Profile document attachment view/download
- [ ] Filename input in support/chat/file form
- [ ] Custom document fetch path on frontend
- [ ] PDF/image previewer input field
- [ ] API that accepts `filename` or `filepath` in JSON body
- [ ] Mobile app API referencing filenames
- [ ] ZIP file extractors (`unzip?target=/uploads`)
- [ ] Dynamic JS import URLs or file names

---

## Archive Extraction & File Operations
- [ ] ZIP/TAR/GZ extraction endpoints
- [ ] Upload + decompress workflows
- [ ] Custom archive builders (with file name templates)
- [ ] File overwrite test in uploads (zip-slip check)
- [ ] Restore/rollback functionality (e.g., `/restore?state=backup.bak`)
- [ ] Log/file rotation input endpoints
- [ ] Backup tools (`?backup=backup.zip`)
- [ ] File mover/renamer (`/rename?file=foo.txt&to=bar.txt`)
- [ ] Script execution with filename input (`/run?script=task.sh`)
- [ ] DB dump loaders (`/load?file=dump.sql`)

---

## HTTP Headers
- [ ] `X-File-Path` (if used internally)
- [ ] `X-Template-Name` (template file path)
- [ ] `X-Theme-Path` (theme loading)
- [ ] `X-Log-Path` or `X-Log-File`
- [ ] `Referer` header if parsed as path
- [ ] `Origin` or `Host` influencing path usage
- [ ] Custom download headers (e.g., `X-Filename`)
- [ ] CDN rewrite headers that inject file paths
- [ ] `Authorization` header as filename token (e.g., `auth-admin.txt`)
- [ ] `Cookie` with stored file paths

---

## JSON, XML, Form & Special Payloads (41–50)
- [ ] JSON body: `{ "file": "../etc/passwd" }`
- [ ] JSON nested: `{ "config": { "path": "../../config.yml" }}`
- [ ] XML parameters (XXE-style): `<file>../../etc/passwd</file>`
- [ ] YAML path inputs
- [ ] Base64-encoded file paths (decoded to traversal)
- [ ] Filepath in cookies or localStorage
- [ ] URL-encoded traversal (`..%2f..%2fetc/passwd`)
- [ ] Double URL encoding (`%252e%252e%252f`)
- [ ] Unicode-encoded traversal (`%c0%ae%c0%ae/`)
- [ ] Form field inputs for filenames (`POST file=../../admin`)

---

## Bonus Tips:
- [ ] Test across `../`, `..%2f`, `..\\`, `..%5c`, `%2e%2e/`, `%252e%252e/`
- [ ] Observe for LFI/RFI escalation: inclusion of PHP/JS files
- [ ] Check log injection paths (`/logs?name=access.log`)
- [ ] Attempt null byte injection (e.g., `.php%00.jpg`)
- [ ] Try traversals to sensitive OS files: `/etc/passwd`, `C:\Windows\win.ini`
- [ ] Combine traversal with file overwrite (zip-slip)

---
