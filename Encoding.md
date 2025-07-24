

> Use these encoding techniques to obfuscate payloads during exploitation (XSS, SQLi, LFI, RCE, SSTI, etc.) to bypass WAF/CDN/firewall filters, custom input sanitizers, or logging mechanisms.

---

## Numeric Representations
- [ ] Decimal encoding (`&#xNNNN;`, `&#DDDD;`)
- [ ] Hexadecimal HTML (`&#x3C;`)
- [ ] Octal encoding (`\074`)
- [ ] Unicode decimal (`\u003c`)
- [ ] Mixed decimal-hex (`\x3c`)
- [ ] Windows-1252 / extended ASCII
- [ ] Java Unicode escapes (`\uXXXX`)
- [ ] UTF-7 encoding (`+ADw-`)
- [ ] UTF-8 overlong encoding (e.g., `C0 AF`)
- [ ] Modified UTF-8 (used in Java)

---

## URL Encodings & Variants
- [ ] Standard percent-encoding (`%3C`)
- [ ] Double URL encoding (`%253C`)
- [ ] Mixed upper/lowercase encoding (`%3c`, `%3C`)
- [ ] Partial encoding (e.g., `jav%61script`)
- [ ] Slash obfuscation (`%2f`, `%5c`)
- [ ] Null byte injection (`%00`)
- [ ] `+` instead of `%20` (space encoding)
- [ ] Unicode normalization bypass (NFC/NFD)

---

## Base Encodings
- [ ] Base64 encoding (`PHNjcmlwdD4=`)
- [ ] Modified Base64 (remove `=` padding)
- [ ] URL-safe Base64
- [ ] Double Base64 encoding
- [ ] Base32 encoding
- [ ] Base36 (e.g., `10` → `A`)
- [ ] Base62 encoding
- [ ] Base85 / Ascii85

---

## Obfuscation Tricks
- [ ] Case flipping (`ScRiPt`)
- [ ] Whitespace injection (`<scr\tipt>`)
- [ ] Comment injection (`<scr<!-- -->ipt>`)
- [ ] JS line breaks (`<scr\nipt>`)
- [ ] Backslash escaping (`\\x3cscript`)
- [ ] JS concatenation: `a='script';eval('<'+a+'>alert(1)</'+a+'>')`
- [ ] Template splitting (e.g., in SSTI)

---

##  Protocol & Format Tricks
- [ ] Data URI encoding (`data:text/html;base64,...`)
- [ ] `javascript:` URI with encoding
- [ ] File path tricks (`..%2f`, `..%c0%af`)
- [ ] Nested encoding (base64 inside hex)
- [ ] MIME-encoding headers
- [ ] XML entity injection (`<!ENTITY xxe SYSTEM "file:///etc/passwd">`)
- [ ] JS char code injection (`String.fromCharCode(88,83,83)`)

---

## Content-Type & Transfer Tricks
- [ ] Chunked Transfer Encoding Smuggling
- [ ] Gzip-compressed payload
- [ ] Multipart/form-data with boundary tricks
- [ ] Content-Type fuzzing (`application/x-www-form-urlencoded; charset=UTF-7`)
- [ ] Transfer-Encoding: mixed-case (`TrAnSfEr-EnCoDiNg`)

---

## Misc Protocol & Filter Bypass
- [ ] Tab/CR/LF injection (`%09`, `%0a`, `%0d`)
- [ ] Zero-width space (`\u200b`, `\uFEFF`)
- [ ] Right-to-left override (`\u202e`)
- [ ] JSON obfuscation (`"na\u006de":`)
- [ ] XML CDATA wrapper (`<![CDATA[<script>]]>`)

---

## Testing Suggestions
- [ ] Create encoded payload matrix per endpoint
- [ ] Compare response diffs with normal vs encoded input
- [ ] Use each encoding with known working payloads
- [ ] Try nested encoding in input fields, headers, and parameters

---

## Tools
- [ ] `CyberChef` – multi-layered encoding
- [ ] `burp decoder` / `decoder tab`
- [ ] `url-encode`, `iconv`, `xxd`, `base64`, `jq` CLI
- [ ] Custom encoder script in Python/Golang