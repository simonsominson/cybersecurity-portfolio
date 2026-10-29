# Password Reset Broken Logic

## Overview
This PortSwigger Web Security Academy lab demonstrates a password reset logic flaw that can lead to account takeover.

## Vulnerability
- **Category:** Authentication
- **Type:** Password Reset Logic Flaw
- **Impact:** Unauthorized password change and potential account takeover

## Methodology
1. Requested a password reset for the controlled `wiener` account.
2. Opened the reset link received through the PortSwigger Email Client.
3. Captured the password-change request using Burp Suite.
4. Modified the client-supplied `username` parameter from `wiener` to `carlos`, while retaining Wiener's reset token.
5. Submitted the modified request.
6. Verified the result by logging in as `carlos` with the new password and accessing the account page.

## Root Cause
The application trusts a client-controlled username parameter to determine which account is modified and fails to enforce a secure association between the reset token and the target account.

## Remediation
- Bind each password-reset token to a specific account on the server.
- Determine the target account from the validated token, not from a client-controlled username.
- Enforce token expiration and single-use validation.
- Invalidate reset tokens after a successful password change.
- Apply rate limiting and monitor suspicious password-reset activity.

## Evidence
Screenshots document the password-reset flow, the original request, the modified request and response, successful access to Carlos's account, and lab completion.

**Note:** Redact session cookies and full reset tokens before publishing screenshots.

## Disclaimer
This report documents testing performed in an intentionally vulnerable PortSwigger Web Security Academy lab for educational purposes.