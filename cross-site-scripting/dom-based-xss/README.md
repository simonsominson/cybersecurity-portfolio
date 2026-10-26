# DOM-Based Cross-Site Scripting (XSS)

## Overview

This report documents a DOM-based Cross-Site Scripting (XSS) vulnerability identified in a PortSwigger Web Security Academy lab.

The application retrieved the `search` parameter from the URL and inserted its value into the page using `innerHTML` without appropriate sanitization. A crafted input triggered JavaScript execution in the browser.

## Vulnerability Details

- **Vulnerability:** DOM-Based Cross-Site Scripting (DOM XSS)
- **Affected component:** Client-side search functionality
- **Source:** URL parameter `search`
- **Sink:** `document.getElementById('searchMessage').innerHTML`
- **Proof of concept:** `<img src=x onerror=alert(1)>`
- **Result:** JavaScript execution confirmed in the lab environment

## Steps to Reproduce

1. Open the lab and submit a search query.
2. Inspect the client-side JavaScript.
3. Identify the flow from the URL's `search` parameter to the `innerHTML` property.
4. Submit the proof-of-concept payload as the search value.
5. Observe the JavaScript alert dialog.

## Impact

The successful proof of concept confirms JavaScript execution in the victim's browser context. Depending on the application's context and security controls, DOM XSS may affect confidentiality and integrity. Additional impacts were not independently demonstrated.

## Root Cause

Untrusted URL input was inserted into an HTML parsing sink (`innerHTML`) without appropriate sanitization or safe DOM handling.

## Remediation

- Use `textContent` when displaying untrusted input as plain text.
- Avoid assigning untrusted data to `innerHTML`.
- If HTML rendering is necessary, use a reputable HTML sanitization library configured with a restrictive allowlist.
- Add security tests to prevent client-side injection vulnerabilities.

## Evidence

Screenshots are stored in the [evidencias/](evidencias/) directory:

- `01-search-request.png` — Baseline search request.
- `02-search-response.png` — JavaScript data flow and vulnerable sink.
- `03-xss-payload-request.png` — Request containing the proof-of-concept payload.
- `04-xss-alert.png` — Confirmation of JavaScript execution.
- `05-lab-solved.png` — Lab completion confirmation.

## Severity

**CVSS:** Not assigned.

A reliable CVSS score requires an assessment of the application's context, exploitability, and demonstrated impact. The alert-based proof of concept alone is insufficient to establish a definitive score.

## Scope

This test was conducted exclusively in a PortSwigger Web Security Academy lab for educational purposes.
