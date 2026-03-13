# Explaination

A command-line tool for detecting CVE-2025-55182 and CVE-2025-66478 in Next.js applications using React Server Components.

For technical details on the vulnerability and detection methodology, see our blog post: https://slcyber.io/research-center/high-fidelity-detection-mechanism-for-rsc-next-js-rce-cve-2025-55182-cve-2025-66478

# How this Works

By default, the scanner sends a crafted multipart POST request containing an RCE proof-of-concept payload that executes a deterministic math operation (41*271 = 11111). Vulnerable hosts return the result in the X-Action-Redirect response header as /login?a=11111.

The scanner tests the root path (/) by default. Use --path or --path-file to test custom paths. If not vulnerable, it follows same-host redirects (e.g., / to /en/) and tests the redirect destination. Cross-origin redirects are not followed.

# OPTIONS

-u, --url         Single URL to check
-l, --list        File containing hosts (one per line)
-t, --threads     Number of concurrent threads (default: 10)
--timeout         Request timeout in seconds (default: 10)
-o, --output      Output file for results (JSON)
--all-results     Save all results, not just vulnerable hosts
-k, --insecure    Disable SSL certificate verification
-H, --header      Custom header (can be used multiple times)
-v, --verbose     Show response details for vulnerable hosts
-q, --quiet       Only output vulnerable hosts
--no-color        Disable colored output
--safe-check      Use safe side-channel detection instead of RCE PoC
--windows         Use Windows PowerShell payload instead of Unix shell
--waf-bypass      Add junk data to bypass WAF content inspection
--waf-bypass-size Size of junk data in KB (default: 128)
--path            Custom path to test (can be used multiple times)
--path-file       File containing paths to test (one per line)
