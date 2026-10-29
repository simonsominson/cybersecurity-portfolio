# Insufficient Workflow Validation

## Overview

This repository documents the PortSwigger Web Security Academy lab **Insufficient workflow validation**, which demonstrates a business logic flaw in an application's purchasing workflow.

The application allowed the purchase confirmation endpoint to be accessed directly without successfully completing the expected checkout process.

## Vulnerability Details

- **Category:** Business Logic Vulnerability
- **Vulnerability:** Insufficient Workflow Validation
- **Target:** `Lightweight l33t leather jacket`
- **Product price:** 1337 units
- **Available account balance:** 100 units
- **Tools:** Burp Suite, Web Browser

## Methodology

1. Inspected the application's purchasing workflow and identified the target product.
2. Attempted to purchase the jacket with insufficient account credit.
3. Observed the server response redirecting to `/cart?err=INSUFFICIENT_FUNDS`.
4. Completed a normal purchase of a cheaper product to identify the successful checkout flow.
5. Identified the confirmation endpoint: `/cart/order-confirmation?order-confirmed=true`.
6. Accessed the confirmation endpoint directly after the checkout rejection.
7. Confirmed that the lab was solved.

## Evidence

Screenshots are available in the [`evidencias/`](evidencias/) directory.

| File | Description |
|---|---|
| `01-initial-page.png` | Initial application page and target product. |
| `02-checkout-request.png` | HTTP checkout request captured with Burp Suite. |
| `03-checkout-response.png` | Server response indicating insufficient funds. |
| `04-successful-checkout.png` | Successful checkout response identifying the confirmation endpoint. |
| `05-successful-purchase.png` | Final purchase confirmation and lab completion. |

## Impact

Insufficient workflow validation can allow users to bypass expected transaction steps. Depending on the application's implementation, this may result in orders being confirmed without proper payment validation, potentially causing financial losses or unauthorized order processing.

The lab demonstrated that the confirmation endpoint could be accessed directly and that the lab was solved. Actual fulfillment of an unpaid order in a production environment was not independently verified.

## Root Cause

The server did not adequately validate the transaction state before allowing access to the order confirmation stage. The application relied on the expected workflow sequence instead of enforcing the required business rules on the server side.

## Remediation

- Enforce all workflow transitions through server-side validation.
- Verify payment authorization and transaction status before confirming an order.
- Associate confirmation requests with valid orders and verified payment states.
- Reject invalid or out-of-sequence state transitions.
- Do not rely on users following the intended page sequence.
- Log and monitor attempts to confirm orders without a valid checkout.

## Disclaimer

This report documents testing performed in an authorized PortSwigger Web Security Academy lab environment. The findings apply to the lab's implementation and should not be interpreted as proof of the same behavior in other applications.