# Vertical Privilege Escalation via User-Controlled Role Parameter

## Overview

This lab demonstrates a vertical privilege escalation vulnerability caused by improper access control enforcement in a web application.

The application relied on a user-controlled role parameter (`Admin=false`) to determine administrative privileges. By changing its value to `Admin=true`, it was possible to access the administrative panel using a standard user account.

The lab was completed by accessing the admin panel and successfully deleting the user `carlos`.

## Vulnerability Details

- **Category:** Broken Access Control
- **Vulnerability:** Vertical Privilege Escalation
- **Affected functionality:** Administrative panel and user management
- **Tool:** Burp Suite Repeater
- **Environment:** PortSwigger Web Security Academy

## Methodology

1. Logged in using a standard user account.
2. Inspected the application's HTTP requests and identified the `Admin=false` role parameter.
3. Modified the parameter to `Admin=true` using Burp Suite Repeater.
4. Accessed the `/admin` endpoint with the modified role value.
5. Confirmed access to administrative functionality.
6. Deleted the user `carlos` and verified the successful operation.
7. Confirmed that the lab was marked as solved.

## Evidence

Screenshots documenting the testing process are available in the `evidencias/` directory.

| Screenshot | Description |
|---|---|
| `01-pagina-inicial.png` | Initial lab page |
| `02-cuenta-usuario.png` | Standard user account |
| `03-peticion-cambio-rol.png` | Modified role parameter |
| `04-acceso-administrativo.png` | Access to the admin panel |
| `05-eliminacion-carlos.png` | User deletion request and HTTP response |
| `06-usuario-eliminado.png` | Successful deletion confirmation |
| `07-laboratorio-resuelto.png` | Lab completion confirmation |

## Impact

An attacker with a standard user account may gain administrative privileges if the application trusts a client-controlled role parameter.

Depending on the available administrative functions, this vulnerability may allow unauthorized access to sensitive information, modification of application data, or deletion of user accounts.

## Root Cause

The application relied on a client-controlled parameter to determine the user's privilege level instead of enforcing authorization through trusted server-side controls.

## Remediation

- Enforce authorization checks on the server for every privileged request.
- Determine user roles and permissions from trusted server-side data.
- Never rely on client-controlled parameters or cookies to grant administrative privileges.
- Apply the principle of least privilege.
- Add access-control tests to prevent privilege escalation regressions.

## Severity

**Estimated severity: High**

The final severity and CVSS score depend on the actual impact, privileges required, and scope of the affected application.

## Disclaimer

This assessment was performed exclusively in the authorized PortSwigger Web Security Academy lab environment for educational purposes.
