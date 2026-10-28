# Server-Side Request Forgery (SSRF)

## Overview
This lab demonstrates a Server-Side Request Forgery (SSRF) vulnerability in a stock-checking functionality. The application accepts a URL through the `stockApi` parameter and makes a server-side request to the specified destination.

By modifying this parameter, it was possible to access an internal administrative panel and delete the user `carlos`.

## Vulnerability Details
- **Vulnerability:** Server-Side Request Forgery (SSRF)
- **Affected endpoint:** `POST /product/stock`
- **Affected parameter:** `stockApi`
- **Target:** `http://127.0.0.1/admin`
- **Severity:** High (provisional assessment)
- **Platform:** PortSwigger Web Security Academy

## Technical Explanation
The application processes a client-controlled URL through the `stockApi` parameter without sufficiently restricting the destination.

The original request used the following URL to retrieve stock information:

`http://stock.weliketoshop.net:8080/product/stock/check?productId=2&storeId=1`

By replacing the URL with `http://127.0.0.1/admin`, the server was induced to access its own internal administrative interface.

This access enabled the execution of an administrative action to delete the user `carlos`, successfully completing the lab.

## Impact
- Access to an internal administrative interface.
- Potential exposure of internal resources.
- Unauthorized modification of application data through an administrative function.
- Possible access to other internal services, depending on the server environment and network configuration.

## Root Cause
The application trusts a URL supplied by the client and performs server-side requests without adequate destination validation or restrictions on access to internal resources.

## Remediation
- Use an allowlist of trusted destinations.
- Avoid accepting complete URLs directly from users when a predefined service identifier can be used instead.
- Validate the URL scheme, hostname, port, and resolved IP address.
- Block requests to localhost, private IP ranges, and unauthorized internal services.
- Restrict outbound network connections through firewall rules and network segmentation.
- Enforce proper authentication and authorization on administrative endpoints.
- Validate redirects and DNS resolution to prevent bypasses of destination restrictions.

## Evidence
Screenshots documenting the testing process and successful lab completion are available in the `evidencias/` directory.

## Disclaimer
This assessment was performed in a controlled PortSwigger Web Security Academy lab environment for educational purposes.