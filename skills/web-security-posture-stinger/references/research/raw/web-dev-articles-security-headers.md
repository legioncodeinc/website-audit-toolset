<!--
URL: https://web.dev/articles/security-headers
Fetch date: 2026-08-18
Source type: official docs (Google)
Research cluster: web-security-posture
Archived by: forge stage 2 sweep (mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc. build sequence step 6.
-->

# Security headers quick reference  |  Articles  |  web.dev
URL: https://web.dev/articles/security-headers

Security headers quick reference | Articles | web.dev

# Security headers quick reference Stay organized with collections Save and categorize content based on your preferences.

Learn more about headers that can keep your site safe and quickly look up the most important details.

Eiji Kitamura

Artur Janc

Maud Nalpas

This article lists the most important security headers you can use to protect your website. Use it to understand web-based security features, learn how to implement them on your website, and as a reference for when you need a reminder.

Security headers recommended for websites that handle sensitive user data: Content Security Policy (CSP) Trusted Types Security headers recommended for all websites: X-Content-Type-Options X-Frame-Options Cross-Origin Resource Policy (CORP) Cross-Origin Opener Policy (COOP) HTTP Strict Transport Security (HSTS) Security headers for websites with advanced capabilities: Cross-Origin Resource Sharing (CORS) Cross-Origin Embedder Policy (COEP)

Known threats on the web

Before diving into security headers, learn about known threats on the web and why you'd want to use these security headers.

Before diving into security headers, learn about known threats on the web and why you'd want to use these security headers.

### Protect your site from injection vulnerabilities

Injection vulnerabilities arise when untrusted data processed by your application can affect its behavior and, commonly, lead to the execution of attacker-controlled scripts. The most common vulnerability caused by injection bugs is cross-site scripting(XSS) in its various forms, including reflected XSS, stored XSS, DOM-based XSS, and other variants.

An XSS vulnerability can typically give an attacker complete access to user data processed by the application and any other information hosted in the same web origin.

Traditional defenses against injections include consistent use of autoescaping HTML template systems, avoiding the use of dangerous JavaScript APIs, and properly processing user data by hosting file uploads in a separate domain and sanitizing user-controlled HTML.

- Use Content Security Policy (CSP) to control which scripts can be executed by your application to mitigate the risk of injections.
- Use Trusted Types to enforce sanitization of data passed into dangerous JavaScript APIs.
- Use X-Content-Type-Options to prevent the browser from misinterpreting the MIME types of your website's resources, which can lead to script execution.

### Isolate your site from other websites

The openness of the web allows websites to interact with each other in ways that can violate an application's security expectations. This includes unexpectedly making authenticated requests or embedding data from another application in the attacker's document, allowing the attacker to modify or read application data.

Common vulnerabilities that undermine web isolation include clickjacking, cross-site request forgery(CSRF), cross-site script inclusion(XSSI), and various cross-site leaks.

- Use X-Frame-Options to prevent your documents from being embedded by a malicious website.
- Use Cross-Origin Resource Policy (CORP) to prevent your website's resources from being included by a cross-origin website.
- Use Cross-Origin Opener Policy (COOP) to protect your website's windows from interactions by malicious websites.
- Use Cross-Origin Resource Sharing (CORS) to control access to your website's resources from cross-origin documents.

Post-Spectre Web Development is a great read if you are interested in these headers.

### Build a powerful website securely

Spectre puts any data loaded into the same browsing context group potentially readable despite same-origin policy. Browsers restrict features that may possibly exploit the vulnerability behind a special environment called " cross-origin isolation". With cross-origin isolation, you can use powerful features such as`SharedArrayBuffer`.

- Use Cross-Origin Embedder Policy (COEP) along with COOP to enable cross-origin isolation.

### Encrypt traffic to your site

Encryption issues appear when an application does not fully encrypt data in transit, allowing eavesdropping attackers to learn about the user's interactions with the application.

Insufficient encryption can arise in the following cases: not using HTTPS, mixed content, setting cookies without the Secure attribute(or__Secure prefix), or lax CORS validation logic.

- Use HTTP Strict Transport Security (HSTS) to consisitently serve your contents through HTTPS.

## Content Security Policy (CSP)

Cross-Site Scripting (XSS) is an attack where a vulnerability on a website allows a malicious script to be injected and executed.

`Content-Security-Policy` provides an added layer to mitigate XSS attacks by restricting which scripts can be executed by the page.

It's recommended that you enable strict CSP using one of the following approaches:

- If you render your HTML pages on the server, use a nonce-based strict CSP.
- If your HTML has to be served statically or cached, for example if it's a single-page application, use a hash-based strict CSP.

Example usage: A nonce-based CSP

```
Content-Security-Policy:
  script-src 'nonce-{RANDOM1}' 'strict-dynamic' https: 'unsafe-inline';
  object-src 'none';
  base-uri 'none';

```

How to use CSP

### Recommended usages

#### 1. Use a nonce-based strict CSP {: #nonce-based-csp}

If you render your HTML pages on the server, use a nonce-based strict CSP.

Generate a new script nonce value for every request on the server side and set the following header:

server configuration file

```
Content-Security-Policy:
  script-src 'nonce-{RANDOM1}' 'strict-dynamic' https: 'unsafe-inline';
  object-src 'none';
  base-uri 'none';
```

In HTML, in order to load the scripts, set the`nonce` attribute of all` ` tags to the same`{RANDOM1}` string.

index.html

```
<script nonce="{RANDOM1}" src="https://example.com/script1.js"></script>
<script nonce="{RANDOM1}">
  // Inline scripts can be used with the <code>nonce</code> attribute.
</script>
```

Google Photos is a good nonce-based strict CSP example. Use DevTools to see how it's used.

#### 2. Use a hash-based strict CSP {: #hash-based-csp}

If your HTML has to be served statically or cached, for example if you're building a single-page application, use a hash-based strict CSP.

server configuration file

```
Content-Security-Policy:
  script-src 'sha256-{HASH1}' 'sha256-{HASH2}' 'strict-dynamic' https: 'unsafe-inline';
  object-src 'none';
  base-uri 'none';
```

In HTML, you'll need to inline your scripts in order to apply a hash-based policy, because most browsers don't support hashing external scripts.

index.html

```
<script>
...// your script1, inlined
</script>
<script>
...// your script2, inlined
</script>
```

To load external scripts, read "Load sourced scripts dynamically" under Option B: Hash-based CSP Response Header section.

CSP Evaluator is a good tool to evaluate your CSP, but at the sam
