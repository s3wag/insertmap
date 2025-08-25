
## 🎯 Goal:
Identify user-controllable inputs that lead to client-side JavaScript vulnerabilities such as prototype pollution, insecure deserialization, sandbox escapes, logic bugs, object injection, insecure eval/function usage, and JS API misuses in real-world web apps.

---

## Prototype Pollution Points
- [ ] `Object.assign({}, userInput)` — no key sanitization
- [ ] `$.extend(true, {}, userInput)`
- [ ] `lodash.merge({}, userInput)` with attacker input
- [ ] Merging objects with `__proto__` from query/cookie
- [ ] Setting `constructor.prototype` via param
- [ ] Unvalidated object merge in SSR template rendering
- [ ] Accepting JSON body with `__proto__` or `prototype` fields
- [ ] Accepting arrays with crafted `__proto__`
- [ ] Importing attacker-controlled JSON into config
- [ ] No filtering on keys like `toString`, `valueOf`, etc.

---

## Function Execution/Injection
- [ ] `eval(userInput)` from query/hash
- [ ] `Function(userInput)` used in business logic
- [ ] `setTimeout(userInput, 0)`
- [ ] `setInterval(userInput, 1000)`
- [ ] Dynamic property access: `obj[userInput]()`
- [ ] Creating functions with `new Function()`
- [ ] Passing user data to template literals inside eval
- [ ] User data passed to global function registry
- [ ] Overriding native prototype methods via input
- [ ] Using `vm.runInNewContext` unsafely

---

## Object Injection/Deserialization
- [ ] Using `JSON.parse(userInput)` directly
- [ ] Parsing user objects in SSR (e.g. Nuxt, Next.js)
- [ ] `Object.keys(userInput).forEach()` w/o validation
- [ ] `for (key in userInput)` — dynamic execution
- [ ] Using `new RegExp(userInput)` with input
- [ ] Using attacker data in YAML/INI to JSON converters
- [ ] Deserializing config/state from localStorage w/o validation
- [ ] Accepting raw JSON from WebSocket without filtering
- [ ] Reading user-injected JavaScript from browser storage
- [ ] Mixing attacker JSON with internal trusted state

---

## JavaScript Engine/Type Confusion Points
- [ ] Using `==` instead of `===` in input comparisons
- [ ] Type coercion in conditional logic
- [ ] `if (userInput)` logic bypass via falsy/truthy values
- [ ] Overriding built-in array methods using polluted prototype
- [ ] Using `with()` statement in legacy JS with input

---

## Framework-Specific Vulnerabilities
- [ ] AngularJS binding with user data `ng-bind-html`
- [ ] Vue.js templates rendered with unescaped input
- [ ] React `dangerouslySetInnerHTML` from location.search
- [ ] Handlebars `{{{triple_braces}}}` with user data
- [ ] Mustache rendering from URL parameter
- [ ] jQuery `$(userInput)` treated as selector
- [ ] Ember rendering templates from user-controlled URL
- [ ] Client-side routers rendering path params into DOM
- [ ] Webpack configs injected with runtime variables
- [ ] Next.js/Remix SSR hydration w/ unsanitized values

---

## JavaScript APIs
- [ ] Using `postMessage(event.data)` without origin validation
- [ ] Listening to `message` events and trusting content
- [ ] Allowing attacker to inject `location.href` in JS redirects
- [ ] Accessing `window.name` or `localStorage` unsafely
- [ ] Not sanitizing inputs used in Service Worker routes

---

## Recommended Payloads to Trigger Bugs
- [ ] `__proto__[alert]=1`
- [ ] `constructor.constructor('alert(1)')()`
- [ ] `javascript:alert(1)`
- [ ] `{"__proto__":{"toString":"alert(1)"}}`
- [ ] `x=alert(1)//`

---
