
##  Insecure JavaScript Practices
- [ ] Sensitive API keys or secrets hardcoded in JS
- [ ] Secrets in commented-out JS code
- [ ] Exposing internal API endpoints in JS files
- [ ] Debugging or test functions left in production scripts
- [ ] Dead code revealing logic or credentials
- [ ] Including third-party scripts from non-trusted CDNs
- [ ] Inline JS that exposes sensitive logic or keys
- [ ] Poorly obfuscated or unminified JS exposing app logic
- [ ] JS source map files (`.map`) exposed publicly
- [ ] API structure or JWT secrets leaked in JS constants

##  Insecure URL and Redirect Handling
- [ ] Insecure `window.location` or `window.open()` usage
- [ ] Trusting `location.hash`, `location.search`, or `location.href` unsafely
- [ ] Open redirect via `location.replace()` or `assign()`
- [ ] Parsing URLs without origin validation
- [ ] Unsafe use of `postMessage` without `origin` check
- [ ] Insecure use of `document.referrer` for auth or redirection logic
- [ ] Exposing sensitive data in URLs (tokens, emails, etc.)
- [ ] Using `eval` or `Function()` with data from the URL
- [ ] Performing logic based on hash fragments (manipulable client-side)
- [ ] Allowing `file://`, `data://`, or `blob://` URLs without restrictions

##  Insecure Client-Side Storage
- [ ] Storing access tokens in `localStorage` or `sessionStorage`
- [ ] Sensitive data (e.g., emails, PII) in `IndexedDB`
- [ ] Storing passwords or secrets in browser storage
- [ ] Not encrypting stored data in offline-capable apps
- [ ] Long-term persistent tokens in cookies with no expiry
- [ ] Exposing session data via `window.name` property
- [ ] Using unprotected Service Workers to cache sensitive data
- [ ] Caching personal/user data without `no-store` directive
- [ ] Syncing sensitive localStorage data across tabs
- [ ] DOM-based key/value storage used as a user trust boundary

## JavaScript Engine & DOM Misuse
- [ ] Unsafe use of `eval`, `setTimeout`, `setInterval`, or `Function()`
- [ ] Using `innerHTML` or `outerHTML` to render untrusted content (not for XSS)
- [ ] Leaking sensitive DOM nodes through JavaScript errors
- [ ] Abusing `Object.prototype` for prototype pollution vectors
- [ ] Exposing internal application state via global variables
- [ ] Unsafe manipulation of `iframe`, `frames`, or `window.opener`
- [ ] JS logic trusting `window.opener` without validation
- [ ] DOM traversal exposing private content (`.shadowRoot`, `.children`)
- [ ] Custom JS events leaking internal app state/data
- [ ] Overwriting built-in DOM properties (`__proto__`, `constructor`, etc.)

## Browser-Specific & UX-Based Attacks
- [ ] Clickjacking-like UI abuse (not frame-based)
- [ ] Autofill vulnerabilities in login/credit card fields
- [ ] Misleading input types allowing browser to autofill hidden fields
- [ ] URL spoofing via `document.title` manipulation
- [ ] Drive-by download logic triggered on page load
- [ ] Clipboard API misuse (auto copy/paste of sensitive data)
- [ ] Screen orientation lock abuse (disorienting users)
- [ ] Abuse of vibration/notification APIs to annoy or phish
- [ ] Using `window.print()` to trick users into printing scam pages
- [ ] History manipulation to lock users in fake navigation loops

## Tips:
- Use browser DevTools > Sources > Search All Files (`Ctrl+Shift+F`) to hunt exposed secrets.
- Use `chrome://net-internals`, `about:debugging`, and `IndexedDB` tabs for deep browser info.
- Check `ServiceWorker`, `manifest.json`, and `sw.js` for offline/caching bugs.
- Review storage in `Application > Local Storage`, `Session Storage`, `Cookies`, `IndexedDB`.
