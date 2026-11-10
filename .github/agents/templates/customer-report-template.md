---
title: "<Category> Certification Test Report"
author: "<Author Name>"
date: "<YYYY-MM-DD>"
---

# Executive Summary

| Total | Passed | Failed | Deferred |
|---|---|---|---|
| 0 | 0 | 0 | 0 |

Short narrative of scope and outcome.

# Environment and Variables

Parameterize these so the test can be re-run in another environment.

| Variable | Description | Value used |
|---|---|---|
| `RESOLVER_IP` | CacheServe resolver address | `<value>` |
| `CLIENT_A` | Load/attack host | `<value>` |
| `CLIENT_B` | Independent availability-check host | `<value>` |

Disclose any lab substitutes here (e.g., dnsdist + keepalived in place of the vendor vLB).

# Test Case Results

## <TEST-ID>: <Title>

- **Objective:** 
- **Commands:**

  ```
  <command>
  ```

- **Measured result:** 
- **Status:** PASS / FAIL
- **Evidence reference:** EV-<TEST-ID>
- **Caveats:** 

# Deferred Test Cases — Detail

## <TEST-ID>: <Title>

- **Blocking dependency:** (e.g., real SAML IdP, customer mTLS topology)
- **Locally verified precondition portion:** 
- **Suggested Test Procedure:**
  1. 
  2. 
  3. 
- **Expected result / pass criteria:** 

# Conclusion

Overall assessment, outstanding items, and recommendations.
