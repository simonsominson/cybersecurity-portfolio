# Server-Side Template Injection (SSTI)

## Description

This lab demonstrates a Server-Side Template Injection (SSTI) vulnerability in the `message` parameter.

The application processes user input as part of a server-side template without properly separating user input from template code.

## Vulnerability

The `message` parameter allows user input to be evaluated by the server-side template engine.

By submitting a mathematical expression, I confirmed that the application evaluated the expression and returned the result.

Further testing in the lab demonstrated that the vulnerability could be used to execute system commands.

## Proof of Concept

1. I identified the `message` parameter as a possible injection point.
2. I submitted the expression `{{7*7}}`.
3. The application returned `49`, confirming that the expression was evaluated on the server.
4. I continued testing and demonstrated command execution within the lab environment.

## Impact

Depending on the template engine and its configuration, SSTI may allow an attacker to:

- Read sensitive information from the server.
- Access internal application data.
- Execute system commands.
- Compromise the confidentiality, integrity, and availability of the application.

The demonstrated impact in this lab includes server-side expression evaluation and command execution.

## Root Cause

The application processes user-controlled input as a template expression without proper isolation between user data and template code.

## Remediation

- Avoid processing user input as template code.
- Use secure template APIs that treat user input as data.
- Apply strict input handling where appropriate.
- Run the application with the minimum required permissions.
- Restrict the template engine's access to sensitive resources and system functions.

## Evidence

Screenshots documenting the testing process and successful lab completion are available in the [`evidencias/`](evidencias/) directory.

## Disclaimer

This report documents testing performed in an authorized PortSwigger Web Security Academy lab environment. All testing was conducted for educational purposes.
