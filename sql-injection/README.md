# SQL Injection (SQLi)

## Overview
This lab demonstrates a SQL Injection vulnerability in the product category filtering functionality of a web application.

By manipulating the `category` parameter, it was possible to alter the logic of the underlying SQL query and retrieve products beyond the originally selected category.

The lab was successfully completed in PortSwigger Web Security Academy.

## Vulnerability Details
- **Vulnerability:** SQL Injection (SQLi)
- **Affected endpoint:** `GET /filter`
- **Affected parameter:** `category`
- **Test payload:** `' OR 1=1--`
- **Severity:** Medium (provisional assessment)
- **Platform:** PortSwigger Web Security Academy

## Technical Explanation
The application uses the `category` parameter to filter products. Supplying a single quote (`'`) resulted in an HTTP `500 Internal Server Error`, indicating a possible issue with how the input was processed.

A subsequent test used the following SQL injection payload:

`' OR 1=1--`

The condition `1=1` is always true, while `--` starts a SQL comment in database systems that support this syntax. This altered the filtering logic and caused the application to return products outside the originally selected category.

The lab displayed the **Solved** status, confirming successful completion.

## Impact
- Bypass of the intended product category filter.
- Unauthorized retrieval of records outside the selected category.
- Potential exposure of additional database information, depending on the affected query and database permissions.

No data modification or deletion was demonstrated in this lab.

## Root Cause
The application processes user-controlled input in an SQL query without adequately separating input data from SQL instructions. This allows a crafted parameter value to alter the intended query logic.

## Remediation
- Use parameterized queries or prepared statements.
- Avoid building SQL queries through string concatenation with user-controlled input.
- Apply the principle of least privilege to database accounts.
- Handle database errors securely and avoid exposing internal details to users.
- Perform security testing to verify that manipulated inputs cannot alter query behavior.

## Evidence
Screenshots documenting the initial application state, original request, SQL error, injection test, and successful lab completion are available in the `evidencias/` directory.

## Disclaimer
This assessment was performed in a controlled PortSwigger Web Security Academy lab environment for educational purposes.