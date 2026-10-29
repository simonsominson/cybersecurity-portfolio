# XXE — Exploiting XXE to Retrieve Files

## Overview

This lab demonstrates an XML External Entity (XXE) vulnerability in the stock-checking functionality of a web application. The XML parser processes an external entity supplied in the request, allowing the application to disclose the contents of a local file.

## Vulnerability Details

- **Category:** XML External Entity (XXE)
- **Endpoint:** `POST /product/stock`
- **Target file:** `/etc/passwd`
- **Tool:** Burp Suite
- **Platform:** PortSwigger Web Security Academy

## Methodology

1. Intercepted the stock-check request using Burp Suite.
2. Sent the request to Repeater for testing.
3. Modified the XML payload to define an external entity referencing `file:///etc/passwd`.
4. Referenced the entity in the `productId` element and sent the modified request.
5. Observed that the server response disclosed the contents of the requested local file.

The server returned `400 Bad Request`, but the response body still exposed the file contents.

## Impact

An attacker may be able to read local files accessible to the application's operating-system user. Depending on the application environment and file permissions, this could expose sensitive system or application data.

## Remediation

- Disable external entity resolution in the XML parser.
- Disable DTD processing when it is not required.
- Use secure XML parser configurations and libraries.
- Apply least-privilege permissions to the application process.
- Add security tests to ensure that external entities cannot access local resources.

## Evidence

Screenshots documenting the original request, the XXE payload and response, and the completed lab are available in the [`evidencias/`](evidencias/) directory.

## Reference

[PortSwigger Web Security Academy — Exploiting XXE to retrieve files](https://portswigger.net/web-security/xxe/lab-exploiting-xxe-to-retrieve-files)

