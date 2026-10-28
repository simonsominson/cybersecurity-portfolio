# Mass Assignment — Checkout Discount Manipulation

## Overview

This project documents a Mass Assignment vulnerability identified in a PortSwigger Web Security Academy lab.

The application exposed a `chosen_discount` object containing a `percentage` property in the checkout API response. By modifying the discount value in a checkout request, I verified that the application accepted client-controlled discount data and successfully completed the lab.

## Vulnerability

- **Category:** Mass Assignment
- **Affected endpoint:** `POST /api/checkout`
- **Parameter:** `chosen_discount.percentage`
- **Tool:** Burp Suite Repeater
- **Environment:** PortSwigger Web Security Academy lab

## Impact

Improper control over discount-related properties may allow users to manipulate checkout pricing, potentially causing unauthorized discounts and financial losses.

## Root Cause

The application failed to properly restrict client-controlled properties used during checkout processing.

## Remediation

- Calculate discounts exclusively on the server.
- Allowlist accepted request properties.
- Validate business rules and user permissions server-side.
- Calculate final prices using trusted server-side values.
- Add regression tests for unauthorized discount manipulation.

## Evidence

Screenshots and the technical report are available in the `evidencias/` directory and `Mass-Assignment.pdf`.

## Disclaimer

This assessment was performed in an authorized PortSwigger Web Security Academy lab environment for educational purposes.