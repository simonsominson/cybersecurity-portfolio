# IDOR — User ID Controlled by Request Parameter

## Overview

- **Platform:** PortSwigger Web Security Academy
- **Vulnerability:** Insecure Direct Object Reference (IDOR)
- **Category:** Broken Access Control
- **Type:** Horizontal privilege escalation
- **Difficulty:** Apprentice
- **Status:** Lab completed

## Description

This lab demonstrates an Insecure Direct Object Reference (IDOR) vulnerability caused by insufficient server-side authorization checks.

The application uses a user-controlled `id` parameter to identify the account whose information is returned. By modifying this parameter from the authenticated user's identifier (`wiener`) to another user's identifier (`carlos`), it was possible to access Carlos's account information, including his API key, without proper authorization.

## Steps to Reproduce

1. Log in using the provided test credentials.
2. Intercept the request to `/my-account` using Burp Suite.
3. Identify the `id` parameter in the request.
4. Modify the parameter from `id=wiener` to `id=carlos`.
5. Send the modified request and inspect the server response.
6. Confirm that the response contains the other user's API key.

## Impact

- **Confidentiality:** Unauthorized access to another user's account information and API key.
- **Integrity:** No integrity impact was demonstrated during this test.
- **Availability:** No availability impact was demonstrated during this test.

The impact of the exposed API key depends on the permissions and functionality associated with it; further impact was not assumed.

## Root Cause

The application relies on a user-controlled identifier without properly verifying whether the authenticated user is authorized to access the requested account.

## Remediation

- Enforce server-side authorization checks for every request that accesses user-specific resources.
- Derive the current user's identity from the authenticated session whenever appropriate.
- Verify object-level permissions before returning sensitive information.
- Avoid relying on client-controlled identifiers as proof of authorization.
- Add automated tests to verify isolation between user accounts.

## Evidence

The `evidencias/` directory contains screenshots documenting:

1. The original account request.
2. The modified request and unauthorized access to Carlos's API key.
3. Successful completion of the lab.

## Severity Assessment

- **Estimated severity:** Medium
- **Estimated CVSS v3.1:** 6.5
- **Vector:** `CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N`

This is a provisional estimate based on the demonstrated confidentiality impact. The final score depends on the real-world context and the capabilities associated with the exposed API key.

## Disclaimer

This assessment was performed in an intentionally vulnerable lab environment provided by PortSwigger Web Security Academy. It was conducted for educational purposes only.
