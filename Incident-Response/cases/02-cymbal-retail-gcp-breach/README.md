# Case 2: Cymbal Retail GCP Data Breach

**Status:** Final report · **Date:** 12 Oct 2026 · **Role:** Associate Cloud Security Analyst

## Summary
An attacker brute-forced SSH/RDP on a public-facing VM (`cc-app-01`), planted malware, found a hand-made service account key, and used the over-privileged default service account to reach unencrypted card data in BigQuery. The data was exfiltrated through a publicly open Cloud Storage bucket. Security Command Center flagged the problems, and PCI DSS 3.2.1 compliance dropped below 100%.

## Attack path
Public IP + open 22/3389 → brute force → malware persistence → service account key → BigQuery → public bucket

## Findings and remediation
| Resource | Severity | Vulnerability | Remediation |
|---|---|---|---|
| Bucket | High | Public ACL | Public access removed |
| Bucket | Medium | Uniform access disabled | Uniform bucket-level access enabled |
| Bucket | Low | Logging disabled | Open |
| VM | High | Public IP | Replacement VM has a private IP only |
| VM | Medium | Secure boot off | Enabled |
| VM | Medium | Default service account | Dedicated service account |
| VM | Medium | Full Cloud API access | Default account detached |
| VM | Low | Malware (bad domain) | VM deleted, rebuilt from trusted snapshot |
| Firewall | High | Open SSH | Limited to IAP range 35.235.240.0/20 |
| Firewall | High | Open RDP | Rule deleted |
| Firewall | Medium | Rule logging off | Enabled |

## Response
**Contain:** stopped and deleted the VM, replaced the open firewall rules, locked down the bucket.
**Recover:** rebuilt as `cc-app-02` with a private IP, secure boot and its own service account.
**Verify:** re-checked SCC.
Supporting screenshots and evidence are included in the PDF report.

## Recommendations
1. No public admin access: use IAP, MFA and org policy.
2. Per-workload service accounts, with no user-managed keys.
3. Encrypt or tokenize card data; enforce public access prevention.
4. Logging on by default, with alerts on compliance drops.

## Still open
Attacker identity and timing, VPC Flow Logs and Audit Logging gaps, and smaller SCC findings.

📄 [Full report (PDF)](report.pdf)
