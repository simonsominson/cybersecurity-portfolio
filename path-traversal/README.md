
# Path Traversal — Unauthorized File Access

## Overview

This project documents a Path Traversal vulnerability identified in a PortSwigger Web Security Academy lab.

During testing, I identified an image-loading endpoint that accepts a `filename` parameter. I then tested whether directory traversal sequences could be used to access files outside the intended image directory.

## Vulnerability Details

- **Category:** Path Traversal
- **Endpoint:** `/image`
- **Parameter:** `filename`
- **Tool:** Burp Suite Repeater
- **Environment:** PortSwigger Web Security Academy

## Impact

Depending on the files accessible to the application, Path Traversal may expose sensitive system or application data.

The demonstrated impact should be assessed according to the actual server response, file permissions, and sensitivity of the retrieved data.

## Root Cause

The application does not adequately restrict user-controlled file paths to the intended directory.

## Remediation

- Avoid using user-supplied file paths directly.
- Map approved identifiers to server-side files.
- Canonicalize and validate file paths.
- Ensure resolved paths remain within the authorized directory.
- Apply least-privilege permissions.
- Add regression tests for directory traversal attempts.

## Evidence

Screenshots and the technical report are available in the `evidencias/` directory and `Path-Traversal.pdf`.

## Disclaimer

This assessment was performed in an authorized PortSwigger Web Security Academy lab environment for educational purposes.
