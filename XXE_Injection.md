
## Check these parameters, APIs, and file upload features for XXE vulnerability

---

## XML-Based API Endpoints
- [ ] /api/xml
- [ ] /xmlrpc.php
- [ ] /rest/xml
- [ ] /soap
- [ ] /services/xml
- [ ] /data/upload/xml
- [ ] /parse/xml
- [ ] /import/xml
- [ ] /convert/xml
- [ ] /report/xml

---

## File Uploads & Import Features
- [ ] XML file import (config, data, etc.)
- [ ] SVG file upload (with embedded XML)
- [ ] DOCX, XLSX, PPTX (unzipped ➜ .xml inside)
- [ ] PDF upload with embedded XML
- [ ] OpenOffice or LibreOffice file uploads (.odt)
- [ ] XML backup restore uploads
- [ ] Invoice/receipt XML uploads
- [ ] Sitemap/XML feed imports
- [ ] ePub or AndroidManifest.xml uploads
- [ ] Form submissions with `application/xml` content

---

## Headers & Content-Type Clues 
- [ ] Content-Type: application/xml
- [ ] Content-Type: text/xml
- [ ] Content-Type: application/soap+xml
- [ ] Accept: application/xml
- [ ] Accept: text/xml
- [ ] X-Content-Type: application/xml
- [ ] SOAPAction header present
- [ ] Request/response shows XML in body
- [ ] File upload hints XML MIME
- [ ] Missing or loose content-type validation

---

## Config and Metadata Imports
- [ ] SAML metadata import (SAML ➜ XML-based)
- [ ] WordPress import/export
- [ ] Jenkins config XML import
- [ ] Shibboleth XML upload
- [ ] Spring config import (XML)
- [ ] XML DTD schema import
- [ ] Feed parsers (RSS, Atom)
- [ ] App settings import via XML
https://github.com/s3wag/insertmap- [ ] IoT/firmware XML config upload
- [ ] Email/SMTP config upload (XML-based)

---

## Third-Party Integrations & Protocols
- [ ] SOAP web services (WSDL)
- [ ] XML-RPC interfaces
- [ ] SAML-based SSO (vulnerable to XXE)
- [ ] BPMN workflow tools (XML-based)
- [ ] SVG viewer components
- [ ] XML used in CI/CD tools (e.g., GitLab pipelines)
- [ ] CRM/ERP XML-based imports
- [ ] UDDI or WSDL-based services
- [ ] XML forms for surveys or insurance apps
- [ ] DITA or XML content authoring tools

---

## Payload Suggestions (XXE Testing Tips)
- [ ] Add `<!DOCTYPE root [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>`
- [ ] Use blind XXE payloads with Interactsh or Burp Collaborator
- [ ] Include remote DTDs to evade filters
- [ ] Use `<!ENTITY % file SYSTEM "..."> %file;` for advanced XXE
- [ ] Inject payloads in XML attributes, tags, and CDATA

---

## Bonus: High-Impact Files for Inclusion
- [ ] file:///etc/passwd
- [ ] file:///c:/windows/win.ini
- [ ] file:///proc/self/environ
- [ ] file:///root/.ssh/id_rsa
- [ ] http://your-collaborator-url.com
- [ ] smb://attacker.com/file
- [ ] gopher://internal:8080
- [ ] zip://evil.zip%23payload.dtd

---
