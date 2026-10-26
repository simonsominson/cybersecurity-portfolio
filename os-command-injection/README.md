# OS Command Injection

## Overview

This report documents an OS Command Injection vulnerability identified in the PortSwigger Web Security Academy lab **OS command injection, simple case**.

The vulnerability affected the stock-check functionality. By modifying the `storeId` parameter in a `POST /product/stock` request, it was possible to execute an operating system command on the server.

## Vulnerability Details

- **Vulnerability:** OS Command Injection
- **Affected endpoint:** `POST /product/stock`
- **Affected parameter:** `storeId`
- **Testing tool:** Burp Suite Repeater
- **Environment:** PortSwigger Web Security Academy
- **Result:** Successful command execution confirmed

## Proof of Concept

The original request contained the following parameters:

```text
productId=2&storeId=1
```

The `storeId` parameter was modified to append a shell command:

```text
productId=2&storeId=1| whoami
```

The server response returned the operating system account name produced by `whoami`. This confirmed that user-controlled input could alter the command executed by the server.

## Evidence

Screenshots collected during the lab are available in the [`evidencias/`](evidencias/) directory.

| File | Description |
|---|---|
| `01-lab-inicial.png` | Initial store page and test context |
| `02-solicitud-stock-original.png` | Original stock-check request |
| `03-respuesta-original.png` | Baseline response showing `200 OK` and stock value `32` |
| `04-command-injection-output.png` | Modified request and command output |
| `05-lab-solved.png` | PortSwigger lab completion confirmation |

## Impact

OS Command Injection can potentially affect all three security properties:

- **Confidentiality:** Commands may expose files and information accessible to the server process.
- **Integrity:** Commands may modify or delete resources available to that process.
- **Availability:** Commands may disrupt the service or consume system resources.

The confirmed result in this lab was execution of `whoami` and disclosure of the operating system account name. Further impacts were not independently tested.

## Root Cause

The application handled user-controlled input unsafely in an operation that executed operating system commands. Shell metacharacters in the `storeId` value were interpreted as command syntax rather than treated strictly as data.

## Remediation

- Avoid invoking an operating system shell when the required operation can be performed through a suitable API or library.
- If an external process is necessary, pass the executable and arguments separately without shell interpretation.
- Validate `storeId` on the server using an allowlist of valid identifiers.
- Run application processes with least privilege.
- Restrict the process's access to files, system resources, and network services.
- Add security tests to verify that user input cannot alter command execution.

## Severity and CVSS

**Provisional severity:** High.

A definitive CVSS score is not assigned based solely on this proof of concept. A reliable score requires evaluating the real exploitation conditions, privileges required, scope, and demonstrated impact.

## Scope and Disclaimer

This test was conducted exclusively in the authorized PortSwigger Web Security Academy educational lab. The result demonstrates the vulnerability in that lab environment and does not establish that any production system is affected.

This report is intended for educational and cybersecurity portfolio purposes.