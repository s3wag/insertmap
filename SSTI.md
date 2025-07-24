
## Target Tech: Jinja2, Twig, Velocity, Freemarker, Smarty, EJS, Handlebars, Razor, Pug, etc.

---

## Authentication / Login / Signup
- [ ] `/login` → `username` or `email` fields rendered in server-side error messages
- [ ] `/register` → `username`, `email`, or `full_name` reflected in templates
- [ ] `/forgot-password` → `email` field rendered in success message
- [ ] Login error message showing part of input (template rendered)
- [ ] `/2fa` or `/verify` → parameter like `code` or `user` reflected
- [ ] Custom messages like `welcome {{user}}` during login/signup
- [ ] `/account/activate` → token or `name` parameter rendered on page
- [ ] `next=`, `returnTo=`, or `redirect_to=` rendered on screen
- [ ] `/complete-profile` → name-based greeting rendered
- [ ] `/invite` → invite message rendered from server

---

## Profile & User Info
- [ ] `/profile` → `bio`, `about`, or `description` fields
- [ ] `/account/settings` → input fields rendered back
- [ ] `/dashboard` → user's `full_name` or `email` reflected
- [ ] User-uploaded info (nickname, company, etc.) rendered server-side
- [ ] Account page title/subtitles contain user-controlled input
- [ ] `/user/{{username}}` → URL-based template rendering
- [ ] `/feedback` or `/support` form with reflected name/email
- [ ] Signature in user comment displayed with template logic
- [ ] `/profile/edit` → pre-filled fields rendered using templates
- [ ] `avatar_url`, `location`, or `status_message` rendered in templates

---

## Messaging / Notification Systems
- [ ] `/message/send` → `message_body` or `subject` reflected
- [ ] Notifications rendered with `{{message.subject}}`
- [ ] `/comments` or `/replies` → comment text rendered in HTML
- [ ] Server-rendered preview of a message or email template
- [ ] Chat applications displaying user input in chat bubbles
- [ ] `/email/preview` → subject/content rendered using templates
- [ ] `/notes` → server-rendered markdown or input
- [ ] `/wall` or `/timeline` posts displayed with templating engine
- [ ] Personalized messages such as “Hello, {{username}}”
- [ ] Email footer or header accepting user-influenced input

---

## API & Backend Logic
- [ ] `/api/preview` → renders template from POST body
- [ ] `/render` → accepts `template` or `data` param
- [ ] `/generate-pdf` → accepts templated HTML input
- [ ] `/invoice/render` → dynamic input reflected
- [ ] `/pdf/export` → fields like `customer_name`, `details`
- [ ] `/ticket/preview` → HTML template preview with injection
- [ ] `/receipt` → input rendered using engine like Twig/Handlebars
- [ ] `/report/preview` → accepts template ID + injected data
- [ ] `/generate-email` → subject and body from user input
- [ ] `/export-html` → free-text rendered using templating

---

## Admin/Customization Features
- [ ] `/admin/announcement` → custom text rendered
- [ ] `/custom-template` → uploadable or editable template
- [ ] CMS with editable page titles/content that gets rendered
- [ ] `/admin/message-builder` → dynamic text builder
- [ ] `/admin/email-builder` → injection via subject or message
- [ ] `/admin/dashboard` → custom widget config stored as templates
- [ ] `/marketing/promo-text` → template variables used
- [ ] `/cms/editor` → template editor with preview
- [ ] `/builder/template-render` → template file + input
- [ ] `/custom-alerts` → input used for generating alerts

---

## Fuzzing Tips
- [ ] Inject `{{7*7}}`, `{{config}}`, `${7*7}`, `<%= 7*7 %>`, `${{7*'7'}}` to test
- [ ] Observe template rendering errors (`TemplateSyntaxError`, etc.)
- [ ] Check for sandbox escape using `__class__`, `self`, `globals`
- [ ] Try payloads in URL params, form fields, headers, and JSON body

---

## Tools
- [ ] `tplmap`
- [ ] `SSTI-Hunter`
- [ ] `Burp Intruder` / `Repeater`
- [ ] Custom fuzzers with template payload lists

---
