
## Objective:
This checklist helps you identify vulnerable JavaScript-controlled DOM sinks that can be manipulated using user-controllable sources like URL fragments, query strings, or cookies — often leading to DOM XSS, client-side open redirects, or logic abuse.

---

## URL-Based DOM Sources (1–10)
- [ ] `location.hash` used in DOM without sanitization
- [ ] `location.search` parsed and injected directly
- [ ] `document.URL` reflected or parsed insecurely
- [ ] `document.documentURI` echoed into HTML/JS
- [ ] `document.location.href` as a sink
- [ ] `window.name` used to modify DOM
- [ ] `new URL(location).searchParams.get()` used insecurely
- [ ] `document.referrer` used in client-side logic
- [ ] `window.location.pathname` parsed and rendered
- [ ] `window.location.origin` manipulated by subdomain control

---

## Dangerous DOM Sinks (11–20)
- [ ] `innerHTML = location.hash`
- [ ] `outerHTML = document.URL`
- [ ] `document.write(location.search)`
- [ ] `document.writeln(location.search)`
- [ ] `element.setAttribute("src", location.hash)`
- [ ] `element.src = location.href`
- [ ] `element.href = document.referrer`
- [ ] `eval(location.hash)`
- [ ] `setTimeout(location.hash)`
- [ ] `Function(location.search)`

---

## Insecure JS Libraries / Templates (21–30)
- [ ] AngularJS sandbox escape via `{{constructor.constructor('alert(1)')()}}`
- [ ] jQuery `$(location.hash)` to selector
- [ ] jQuery `$(html)` rendering from URL param
- [ ] Handlebars.js dynamic rendering from `search`
- [ ] Vue.js templates in DOM + unsanitized input
- [ ] Mustache template with attacker input
- [ ] ReactJS dangerouslySetInnerHTML using untrusted data
- [ ] KnockoutJS rendering controlled by `hash`
- [ ] Ember.js `{{unescapedInput}}` via URL
- [ ] URL-controlled rendering in client-side routers (e.g. Angular, Vue)

---

# DOM Clobbering Opportunities (31–40)
- [ ] `?id=form` (clobbers `document.forms`)
- [ ] `?submit=evil` (clobbers form submit function)
- [ ] `?cookie=document` (object property clobbering)
- [ ] Using `iframe.name` for object overriding
- [ ] Clobber `location` by injecting malformed DOM
- [ ] `document.all` manipulation via element ID
- [ ] Overriding `window.alert` via clobbering
- [ ] `?constructor=alert` (constructor hijack)
- [ ] `?__proto__=payload` prototype pollution attempt
- [ ] `?toString=alert` affecting native methods

---

## Client-Side Open Redirects (41–45)
- [ ] `window.location = location.search`
- [ ] `location.href = getParam("redirect")`
- [ ] `window.open(getParam("target"))`
- [ ] `document.location = queryParam("next")`
- [ ] `location.replace(queryParam("url"))`

---

## Cookie / Storage-Based DOM Sources (46–50)
- [ ] `document.cookie` parsed directly into DOM
- [ ] `localStorage.getItem("payload")` used in HTML
- [ ] `sessionStorage.getItem("html")` inserted to DOM
- [ ] `window.name` reflected in the page
- [ ] `IndexedDB` or `Cache API` used with tainted values

---

## Bonus Detection Tips
- [ ] Search for `innerHTML`, `eval`, `Function` in JS files
- [ ] Use tools like DOM Invader (Burp Suite) or DOM XSS Scanner
- [ ] Always test with payloads like:
  - `<img src=x onerror=alert(1)>`
  - `"><svg/onload=alert(1)>`
  - `javascript:alert(document.domain)`
  - `{{constructor.constructor('alert(1)')()}}`

---
