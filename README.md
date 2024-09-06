# Next.js Build Manifest Detection Template

## Overview

This Nuclei template is designed to detect the presence of the `__BUILD_MANIFEST` object on Next.js websites. The `__BUILD_MANIFEST` contains the paths (`sortedPages`) of the pages available on the website. By identifying this, you can gather information on all the accessible routes of the site.

## Template Details

- **Template ID**: nextjs-build-manifest-detection
- **Severity**: Informational
- **Author**: s1d6p01nt7

### Description

The template sends a `GET` request to the target's base URL and checks for the presence of `__BUILD_MANIFEST` and `sortedPages` within the HTML or JavaScript response. If these are found, it extracts the paths from the `sortedPages` array.

## Security Implications

### Why This Matters

The presence of the `__BUILD_MANIFEST` object in a Next.js application could have the following security implications:

1. **Unintended Exposure of Routes**: 
   - The `__BUILD_MANIFEST` contains a list of all the pages in the application, including potentially sensitive or hidden routes that developers might not intend to expose to end-users. This could lead to the discovery of admin pages, API endpoints, or test environments that are not properly secured or obscured.
   
2. **Facilitating Reconnaissance**: 
   - Attackers can use this information to map out the entire application structure and target specific endpoints for further attacks, such as brute force, parameter tampering, or exploitation of known vulnerabilities in the discovered routes.
   
3. **Breach of Privacy or Security**:
   - If the `sortedPages` object reveals dynamic routes (e.g., `/user/[id]`, `/order/[id]`), attackers might infer the internal logic of the application, potentially giving them clues about how to manipulate input and gain access to other users' data.

### Risk Assessment

While this exposure is typically classified as an **informational** severity issue, it can escalate if sensitive routes or user-specific data are accessible. The risk increases significantly in cases where:
- There are misconfigured access controls on certain pages.
- Sensitive endpoints, such as administrative panels or debugging interfaces, are inadvertently exposed.

To mitigate this issue, developers should ensure that:
- Routes to sensitive pages are properly secured and hidden from the `__BUILD_MANIFEST`.
- Dynamic routes do not expose information that could be abused by attackers.

## Usage

To use this template with Nuclei, save the YAML file in your Nuclei templates directory and run the following command:

```bash
nuclei -t /path/to/nextjs-build-manifest-detection.yaml -u https://target-website.com




Disclaimer

This template is intended for legal, ethical testing purposes only. Unauthorized or malicious use of this template may violate legal and privacy regulations, including, but not limited to, the Computer Fraud and Abuse Act (CFAA) and the General Data Protection Regulation (GDPR). Ensure that you have explicit permission to test the target systems before running this template. The author and contributors to this template are not responsible for any damage, loss, or legal consequences resulting from misuse.
