<!--
URL: https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html
Fetch date: 2026-08-18
Source type: official docs (OWASP)
Research cluster: web-security-posture
Archived by: forge stage 2 sweep (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc. build sequence step 6.
-->

# HTTP Headers - OWASP Cheat Sheet Series
URL: https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html

HTTP Headers - OWASP Cheat Sheet Series

Skip to content

# HTTP Security Response Headers Cheat Sheet¶

## Introduction¶

HTTP Headers are a great booster for web security with easy implementation. Proper HTTP response headers can help prevent security vulnerabilities like Cross-Site Scripting, Clickjacking, Information disclosure and more.

In this cheat sheet, we will review all security-related HTTP headers, recommended configurations, and reference other sources for complicated headers.

## Security Headers¶

### X-Frame-Options¶

The`X-Frame-Options` HTTP response header can be used to indicate whether or not a browser should be allowed to render a page in a` `,` `,` ` or` `. Sites can use this to avoid clickjacking attacks, by ensuring that their content is not embedded into other sites.

Content Security Policy (CSP) frame-ancestors directive obsoletes X-Frame-Options for supporting browsers (source).

X-Frame-Options header is only useful when the HTTP response where it is included has something to interact with (e.g. links, buttons). If the HTTP response is a redirect or an API returning JSON data, X-Frame-Options does not provide any security.

#### Recommendation¶

Use Content Security Policy (CSP) frame-ancestors directive if possible.

Do not allow displaying of the page in a frame.

`X-Frame-Options: DENY`

### X-XSS-Protection¶

The HTTP`X-XSS-Protection` response header is a feature of Internet Explorer, Chrome, and Safari that stops pages from loading when they detect reflected cross-site scripting (XSS) attacks.

WARNING: Even though this header can protect users of older web browsers that don't yet support CSP, in some cases, this header can create XSS vulnerabilities in otherwise safe websites source.

#### Recommendation¶

Use a Content Security Policy (CSP) that disables the use of inline JavaScript.

Do not set this header or explicitly turn it off.

`X-XSS-Protection: 0`

Please see Mozilla X-XSS-Protection for details.

### X-Content-Type-Options¶

The`X-Content-Type-Options` response HTTP header is used by the server to indicate to the browsers that the MIME types advertised in the Content-Type headers should be followed and not guessed.

This header is used to block browsers' MIME type sniffing, which can transform non-executable MIME types into executable MIME types (MIME Confusion Attacks).

#### Recommendation¶

Set the Content-Type header correctly throughout the site.

`X-Content-Type-Options: nosniff`

### Referrer-Policy¶

The`Referrer-Policy` HTTP header controls how much referrer information (sent via the Referer header) should be included with requests.

#### Recommendation¶

Referrer policy has been supported by browsers since 2014. Today, the default behavior in modern browsers is to no longer send all referrer information (origin, path, and query string) to the same site but to only send the origin to other sites. However, since not all users may be using the latest browsers we suggest forcing this behavior by sending this header on all responses.

`Referrer-Policy: strict-origin-when-cross-origin`

- NOTE: For more information on configuring this header please see Mozilla Referrer-Policy.

### Content-Type¶

The`Content-Type` representation header is used to indicate the original media type of the resource (before any content encoding is applied for sending). If not set correctly, the resource (e.g. an image) may be interpreted as HTML, making XSS vulnerabilities possible.

Although it is recommended to always set the`Content-Type` header correctly, it would constitute a vulnerability only if the content is intended to be rendered by the client and the resource is untrusted (provided or modified by a user).

#### Recommendation¶

`Content-Type: text/html; charset=UTF-8`

- NOTE: the`charset` attribute is necessary to prevent XSS in HTML pages
- NOTE: the`Content-Type` can be any of the possible MIME types

### Cache-Control¶

The`Cache-Control` header defines how responses are cached by browsers and intermediate caches.

#### Recommendation¶

- Use`no-store` for sensitive data to prevent any form of caching.
- Use`private` to allow caching only in non-shared (user-specific) caches and to prevent storage in shared caches (note that private caches may still persist the response).
- Avoid relying on default caching behavior for sensitive or protected content.
- Be aware that`no-cache` does not prevent caching; it allows caches to store responses. It requires revalidation with the origin server before reuse.

These directives help reduce the risk of sensitive data being stored or exposed through caching, but use`no-store` when storage of sensitive data must be strictly prevented.

#### References¶

### Set-Cookie¶

The`Set-Cookie` HTTP response header is used to send a cookie from the server to the user agent, so the user agent can send it back to the server later. To send multiple cookies, multiple Set-Cookie headers should be sent in the same response.

This is not a security header per se, but its security attributes are crucial.

#### Recommendation¶

- Please read Session Management Cheat Sheet for a detailed explanation on cookie configuration options.

### Strict-Transport-Security (HSTS)¶

The HTTP`Strict-Transport-Security` response header (often abbreviated as HSTS) instructs browsers to only access the website using HTTPS, even if a user attempts to connect over HTTP.

#### Recommendation¶

`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

- NOTE: Read carefully how this header works before using it. If the HSTS header is misconfigured or if there is a problem with the SSL/TLS certificate being used, legitimate users might be unable to access the website. For example, if the HSTS header is set to a very long duration and the SSL/TLS certificate expires or is revoked, legitimate users might be unable to access the website until the HSTS header duration has expired.

Please check out HTTP Strict Transport Security Cheat Sheet for more information.

### Expect-CT ❌¶

The`Expect-CT` header lets sites opt-in to reporting of Certificate Transparency (CT) requirements. Given that mainstream clients now require CT qualification, the only remaining value is reporting such occurrences to the nominated report-uri value in the header. The header is now less about enforcement and more about detection/reporting.

#### Recommendation¶

Do not use it. Mozilla recommends avoiding it, and removing it from existing code if possible.

### Content-Security-Policy (CSP)¶

Content Security Policy (CSP) is a security feature that is used to specify the origin of content that is allowed to be loaded on a website or in a web application. It is an added layer of security that helps to detect and mitigate certain types of attacks, including Cross-Site Scripting (XSS) and data injection attacks. These attacks are used for everything from data theft to site defacement to distribution of malware.

- NOTE: This header is relev
