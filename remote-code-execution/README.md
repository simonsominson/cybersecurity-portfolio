# Remote Code Execution via Web Shell Upload

## Overview

This lab demonstrates a file upload vulnerability that allows an attacker to upload a PHP file and execute server-side code.

The application accepts a PHP file through the avatar upload functionality and stores it in a publicly accessible location. By accessing the uploaded file, it is possible to execute PHP code on the server and read a sensitive file.

## Lab Information

- **Platform:** PortSwigger Web Security Academy
- **Category:** File Upload Vulnerabilities
- **Vulnerability:** Remote Code Execution (RCE)
- **Tools:** Burp Suite, Web Browser
- **Difficulty:** Apprentice
- **Status:** Solved

## Technical Summary

The avatar upload functionality accepts a user-controlled file without adequately preventing server-side script execution.

The upload request was intercepted and modified using Burp Suite. A PHP file named `avatar.php` was uploaded successfully and stored at `avatars/avatar.php`.

Accessing the uploaded file confirmed that the server executed the supplied PHP code. The web shell was then used to read the target file specified by the lab, demonstrating access to sensitive server-side data.

## Impact

Successful exploitation may allow an attacker to:

- Execute arbitrary PHP code within the privileges of the web server process.
- Read sensitive files accessible to that process.
- Potentially modify application resources or affect service availability, depending on the process permissions and server configuration.

## Root Cause

The application does not adequately restrict uploaded files from being interpreted as executable server-side scripts.

File extensions and client-supplied MIME types alone are insufficient to validate uploaded content.

## Remediation

- Allow only explicitly permitted file formats and validate the actual file content.
- Store uploaded files outside the web root whenever possible.
- Disable script execution in directories used for uploaded files.
- Generate server-side filenames instead of trusting user-supplied filenames.
- Apply least-privilege permissions to the web server process.
- Restrict access to sensitive files and directories.

## Evidence

Screenshots documenting the lab workflow are available in the [`evidencias/`](evidencias/) directory.

The evidence includes the original upload request, the modified PHP upload, confirmation of PHP execution, the file-read result with sensitive content redacted, and the final solved status.

## Report

The detailed report in Spanish is available here:

[RCE.pdf](RCE.pdf)

## Reference

[PortSwigger Web Security Academy — Remote code execution via web shell upload](https://portswigger.net/web-security/file-upload/lab-file-upload-remote-code-execution-via-web-shell-upload)
