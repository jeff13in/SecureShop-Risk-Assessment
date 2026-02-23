# Compliance Framework Mapping Document
## SecureShop E-Commerce Platform

**Date:** January 2026  
**Author:** Jeffin Sam Joji  
**Purpose:** Map identified security risks to regulatory requirements and industry standards

---

## 1. PCI-DSS v4.0 Compliance Mapping

### Overview
Payment Card Industry Data Security Standard (PCI-DSS) applies to all entities that store, process, or transmit cardholder data.

**Current Compliance Level:** 15% (3 of 20 major requirements met)  
**Merchant Level:** Level 2 (processes 1-6 million transactions/year)  
**Compliance Deadline:** Must achieve 100% to process payments  
**Penalty for Non-Compliance:** $5,000-$100,000/month + potential card brand sanctions

---

### Requirement 1: Install and Maintain Network Security Controls

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 1.2.1 | Firewall configuration standards documented | ⚠️ Partial | No formal change control | PR.PT-01 | Document firewall standards, implement change management |
| 1.3.1 | Network segmentation implemented | ❌ Failed | Flat network architecture | ID.AM-01 | Segment PCI environment (DMZ, cardholder data zone) |
| 1.4.1 | Anti-spoofing measures | ⚠️ Partial | Ingress filtering only | PR.PT-01 | Implement egress filtering, deploy WAF |

**Priority Actions:**
1. Deploy AWS WAF with OWASP ruleset (addresses PR.PT-01)
2. Implement network segmentation using VPCs and security groups
3. Document firewall configuration standards and approval process

---

### Requirement 3: Protect Stored Account Data

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 3.4.1 | PAN rendered unreadable | ❌ **CRITICAL** | Storing plaintext cardholder data | PR.DS-01 | **Implement tokenization - do NOT store PAN** |
| 3.5.1 | Cryptographic keys managed securely | ❌ Failed | Keys in source code | PR.AC-04 | Deploy AWS Secrets Manager/KMS |
| 3.6.1 | Key management procedures documented | ❌ Failed | No procedures exist | PR.AC-04 | Document key lifecycle management |

**CRITICAL ISSUE:** Currently storing full Primary Account Number (PAN) in database  
**Violation:** PCI-DSS Requirement 3.4 - account data must be unreadable  
**Immediate Action Required:** Implement payment tokenization through gateway

**Remediation Steps:**
1. Integrate Stripe/Braintree tokenization API (eliminates need to store cardholder data)
2. Migrate existing stored PANs to tokens (with gateway vendor support)
3. Purge all cardholder data from databases
4. Update application to use tokens for recurring payments
5. Implement Point-to-Point Encryption (P2PE) for card entry

**Timeline:** 30 days (this blocks payment processing capability)  
**Cost:** $15,000 (integration + migration)

---

### Requirement 6: Develop and Maintain Secure Systems and Software

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 6.2.1 | Inventory of bespoke software | ⚠️ Partial | Incomplete inventory | ID.AM-01 | Complete application inventory |
| 6.3.1 | Security vulnerabilities identified | ❌ Failed | No vulnerability scanning | PR.PT-01 | Implement Snyk/OWASP Dependency-Check |
| 6.4.1 | Public-facing web apps protected | ❌ Failed | No WAF deployed | PR.PT-01 | Deploy AWS WAF |
| 6.5.1 | Secure coding practices | ⚠️ Partial | No SAST/DAST in pipeline | ID.RA-01 | Integrate SonarQube, run OWASP ZAP |

**Key Gaps:**
- No automated vulnerability scanning (Requirement 6.3.1)
- No Web Application Firewall (Requirement 6.4.1)
- No secure coding training for developers (Requirement 6.5.1)

---

### Requirement 8: Identify Users and Authenticate Access

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 8.3.1 | Multi-factor authentication for admin access | ❌ **CRITICAL** | No MFA deployed | PR.AC-01 | Deploy Okta/Azure AD MFA |
| 8.4.1 | MFA for all remote network access | ❌ Failed | VPN has password-only auth | PR.AC-01 | Implement MFA on VPN |
| 8.6.1 | Password complexity enforced | ⚠️ Partial | Weak requirements (8 chars) | PR.AC-01 | Enforce 12+ chars, complexity rules |

**CRITICAL ISSUE:** Administrative accounts use password-only authentication  
**Risk:** Account takeover via credential stuffing, phishing, brute force  
**Immediate Action:** Deploy MFA within 30 days

---

### Requirement 10: Log and Monitor All Access

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 10.2.1 | Audit trail for all system components | ⚠️ Partial | Logging incomplete | DE.CM-01 | Centralize logs in AWS CloudWatch |
| 10.4.1 | Audit logs reviewed daily | ❌ Failed | No log review process | DE.CM-01 | Deploy SIEM (Splunk/Security Hub) |
| 10.6.1 | Logs protected from alteration | ❌ Failed | Logs on same server | DE.CM-01 | Forward to immutable log storage |

**Gap Analysis:**
- Logs exist but not centralized (manual review impossible)
- No SIEM solution to correlate events and detect anomalies
- Log integrity not protected (can be modified/deleted by attacker)

---

### Requirement 11: Test Security of Systems Regularly

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 11.3.1 | External vulnerability scans quarterly | ❌ Failed | No scanning program | PR.PT-02 | Subscribe to Qualys/Tenable |
| 11.3.2 | Internal vulnerability scans quarterly | ❌ Failed | No scanning program | PR.PT-02 | Deploy internal scanner |
| 11.4.1 | Penetration testing annually | ❌ Failed | Never conducted | ID.RA-01 | Engage third-party for pentest |

---

### Requirement 12: Support Information Security with Organizational Policies

| Sub-Req | Description | Status | Gap | Associated Risk | Remediation |
|---------|-------------|--------|-----|-----------------|-------------|
| 12.10.1 | Incident response plan documented | ❌ **CRITICAL** | No IR plan exists | RS.CO-01 | Develop IR playbooks (NIST 800-61) |
| 12.10.2 | IR plan tested annually | ❌ Failed | N/A - no plan | RS.CO-01 | Conduct tabletop exercises quarterly |

---

### PCI-DSS Summary

| Status | Count | % |
|--------|-------|---|
| ✅ Compliant | 3 | 15% |
| ⚠️ Partial | 7 | 35% |
| ❌ Non-Compliant | 10 | 50% |

**Critical Blockers (must fix to process payments):**
1. Storing cardholder data (Req 3.4) → **Implement tokenization**
2. No MFA on admin accounts (Req 8.3) → **Deploy MFA**
3. No incident response plan (Req 12.10) → **Develop IR plan**

**Estimated Time to Compliance:** 6-9 months  
**Estimated Cost:** $65,000 (includes QSA assessment)

---

## 2. GDPR Compliance Mapping

### Overview
General Data Protection Regulation (GDPR) protects EU citizen personal data. Applies if you have EU customers.

**Current Compliance Level:** 20%  
**Maximum Fine:** €20M or 4% of global annual revenue (whichever is higher)  
**Key Risks:** No breach notification procedure, indefinite data retention

---

### Article 5: Principles of Processing Personal Data

| Principle | Description | Status | Gap | Associated Risk | Remediation |
|-----------|-------------|--------|-----|-----------------|-------------|
| Art 5(1)(a) | Lawfulness, fairness, transparency | ⚠️ Partial | Privacy policy outdated | PR.DS-03 | Update privacy policy, obtain explicit consent |
| Art 5(1)(b) | Purpose limitation | ⚠️ Partial | Broad consent language | PR.DS-03 | Specify exact purposes for data collection |
| Art 5(1)(c) | Data minimization | ⚠️ Partial | Collecting unnecessary fields | PR.DS-03 | Review data collection forms, remove unnecessary fields |
| Art 5(1)(d) | Accuracy | ⚠️ Partial | No data accuracy verification | PR.DS-03 | Implement periodic data verification prompts |
| Art 5(1)(e) | **Storage limitation** | ❌ **Failed** | Indefinite data retention | PR.DS-03 | Implement 7-year retention with auto-delete |
| Art 5(1)(f) | Integrity and confidentiality | ❌ Failed | No encryption at rest | PR.DS-04 | Enable database encryption |

**Critical Gap:** No data retention policy (Article 5(1)(e))  
**Violation:** Personal data stored indefinitely without business justification  
**Action Required:** Implement automated data deletion after 7 years (or as legally required)

---

### Article 15-22: Data Subject Rights

| Right | Description | Status | Gap | Associated Risk | Remediation |
|-------|-------------|--------|-----|-----------------|-------------|
| Art 15 | Right of access (data portability) | ⚠️ Partial | Manual export process | - | Build self-service data export |
| Art 16 | Right to rectification | ✅ Pass | Users can update profiles | - | No action needed |
| Art 17 | Right to erasure ("right to be forgotten") | ❌ Failed | No deletion workflow | PR.DS-03 | Implement account deletion API |
| Art 18 | Right to restriction of processing | ❌ Failed | Cannot restrict processing | - | Build processing restriction flag |
| Art 20 | Right to data portability | ⚠️ Partial | Manual CSV export | - | Automate machine-readable exports (JSON) |
| Art 21 | Right to object | ⚠️ Partial | Can opt-out of marketing | - | Extend to all processing types |

**Key Implementation:**  
Article 17 (Right to Erasure) requires automated account/data deletion workflow:
1. Build "Delete My Account" feature in user portal
2. Cascade delete all associated data (orders, addresses, payment methods)
3. Anonymize transaction history (cannot delete for legal compliance, but pseudonymize)
4. Send confirmation email
5. Complete within 30 days of request

---

### Article 25: Data Protection by Design and Default

| Requirement | Status | Gap | Associated Risk | Remediation |
|-------------|--------|-----|-----------------|-------------|
| Privacy by Design | ❌ Failed | No Privacy Impact Assessments | ID.RA-01 | Conduct PIA before new features |
| Privacy by Default | ⚠️ Partial | Default settings overly permissive | - | Change defaults to minimal data collection |
| Pseudonymization | ❌ Failed | No pseudonymization techniques | PR.DS-04 | Implement data masking for analytics |

**Action Required:** Conduct Privacy Impact Assessment (PIA/DPIA) for high-risk processing:
- Payment processing (involves financial data)
- Customer profiling (if using analytics for targeting)
- Automated decision-making (if any)

---

### Article 30: Records of Processing Activities

| Requirement | Status | Gap | Associated Risk | Remediation |
|-------------|--------|-----|-----------------|-------------|
| Data processing register | ❌ Failed | No register exists | Compliance | Document all processing activities |
| Controller/processor distinction | ⚠️ Partial | Unclear for third parties | ID.RA-02 | Classify vendors as processors/controllers |

**Required Documentation:**
1. What personal data is collected (name, email, address, payment info, browsing history)
2. Purpose of processing (account creation, payment, marketing, analytics)
3. Legal basis (consent, contract, legitimate interest)
4. Recipients of data (payment gateway, email provider, analytics vendor)
5. Retention periods (7 years for transactions, 2 years for marketing)
6. Security measures (encryption, access controls, logging)

---

### Article 32: Security of Processing

| Requirement | Status | Gap | Associated Risk | Remediation |
|-------------|--------|-----|-----------------|-------------|
| Encryption of personal data | ❌ Failed | Database not encrypted | PR.DS-04 | Enable TDE on PostgreSQL |
| Pseudonymization | ❌ Failed | No techniques implemented | PR.DS-04 | Tokenize identifiers in analytics |
| Ability to restore availability (backups) | ⚠️ Partial | Backups exist but not tested | RC.RP-01 | Test backup restoration quarterly |
| Testing security measures | ❌ Failed | No security testing program | PR.PT-02 | Implement quarterly pentests |

---

### Article 33: Breach Notification to Supervisory Authority

| Requirement | Status | Gap | Associated Risk | Remediation |
|-------------|--------|-----|-----------------|-------------|
| Notify DPA within 72 hours | ❌ **CRITICAL** | No breach notification procedure | RS.CO-01 | Develop breach notification templates |
| Document all breaches | ❌ Failed | No breach register | RS.CO-01 | Create breach incident log |

**CRITICAL GAP:** No breach notification procedure  
**GDPR Requirement:** Must notify Data Protection Authority (DPA) within 72 hours of discovering a breach  
**Penalty for Late/Missing Notification:** Up to €10M or 2% of revenue

**Required Documentation:**
1. Breach notification letter template (to DPA)
2. Customer notification template (if high risk to individuals)
3. Breach assessment decision tree (when to notify)
4. Internal escalation procedure (how security team reaches legal/executive)

---

### Article 44-49: International Data Transfers

| Requirement | Status | Gap | Associated Risk | Remediation |
|-------------|--------|-----|-----------------|-------------|
| Adequacy decision or safeguards | ⚠️ Partial | US-based cloud (AWS) | - | Rely on Standard Contractual Clauses (SCCs) |
| Transfer Impact Assessment | ❌ Failed | Not conducted | - | Assess third-country transfer risks |

**Current Risk:** Using AWS US regions for EU customer data  
**Compliance Mechanism:** AWS provides Standard Contractual Clauses (SCCs) in DPA  
**Action Required:** Review AWS Data Processing Addendum (DPA) for SCCs

---

### GDPR Summary

| Article | Topic | Status | Priority |
|---------|-------|--------|----------|
| Art 5(1)(e) | Data retention | ❌ Failed | HIGH |
| Art 17 | Right to erasure | ❌ Failed | HIGH |
| Art 25 | Privacy by design | ❌ Failed | HIGH |
| Art 30 | Processing register | ❌ Failed | MEDIUM |
| Art 32 | Security measures | ❌ Failed | HIGH |
| Art 33 | Breach notification | ❌ **CRITICAL** | CRITICAL |

**Estimated Time to Compliance:** 4-6 months  
**Estimated Cost:** $35,000 (legal review + technical implementation)

---

## 3. OWASP Top 10 (2021) Compliance Mapping

### A01:2021 - Broken Access Control

**Description:** Users can access resources or perform actions outside their intended permissions.

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| No session timeout | ❌ Failed | PR.AC-03 | Sessions persist indefinitely | Implement 30-min idle, 8-hour absolute timeout |
| Admin functions accessible without authorization check | ❌ Failed | PR.AC-01 | `/admin/users` returns data without auth | Add authorization middleware to all admin routes |
| Direct object references (IDOR) | ⚠️ Warning | - | Can access other users' orders by changing ID | Implement ownership verification in queries |

**Test Case:**
```bash
# Test 1: Session timeout
curl -H "Cookie: session_id=abc123" https://secureshop.com/api/profile
# After 60 minutes, session still valid ❌

# Test 2: Admin access without authorization
curl https://secureshop.com/admin/users
# Returns user list without authentication ❌

# Test 3: IDOR vulnerability
# Logged in as user_id=100
curl https://secureshop.com/api/orders/50
# Returns order details for user_id=75 ❌
```

**Recommendation:**
- Configure session timeout: 30-minute idle, 8-hour absolute
- Add role-based access control (RBAC) middleware
- Validate ownership before returning resources

---

### A02:2021 - Cryptographic Failures

**Description:** Sensitive data exposed due to lack of encryption or weak cryptographic implementation.

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| Database encryption at rest disabled | ❌ Failed | PR.DS-04 | PostgreSQL TDE not enabled | Enable RDS encryption |
| Storing cardholder data | ❌ **CRITICAL** | PR.DS-01 | Full PAN in `payment_methods` table | Implement tokenization |
| Secrets in source code | ❌ Failed | PR.AC-04 | AWS keys committed to GitHub | Rotate keys, use Secrets Manager |
| HTTP used for admin panel | ❌ Failed | - | Admin pages load over HTTP | Enforce HTTPS redirect |

**Test Case:**
```sql
-- Database encryption check
SELECT name, encryption FROM pg_database WHERE name = 'secureshop';
-- Result: encryption = 'off' ❌

-- Cardholder data in database
SELECT card_number FROM payment_methods LIMIT 1;
-- Result: 4532 1234 5678 9010 (full PAN stored) ❌
```

**Recommendation:**
- **Priority 1:** Eliminate cardholder data storage (tokenize via Stripe)
- Enable AWS RDS encryption (requires snapshot restore migration)
- Implement AWS Secrets Manager for API keys
- Enforce HTTPS with HSTS headers

---

### A03:2021 - Injection

**Description:** Untrusted data sent to interpreter (SQL, OS commands, LDAP, etc.)

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| SQL injection in search | ⚠️ Warning | - | Input validation exists but incomplete | Add prepared statements for all queries |
| NoSQL injection possible | ❌ Failed | - | MongoDB query allows object injection | Sanitize user input before queries |
| OS command injection | ✅ Pass | - | No user input passed to shell commands | Continue monitoring |

**Test Case:**
```bash
# SQL injection test (search endpoint)
curl "https://secureshop.com/api/search?query=test' OR '1'='1"
# Parameterized queries used ✅

# NoSQL injection test
curl -X POST https://secureshop.com/api/products \
  -d '{"price": {"$gt": 0}}'
# Returns all products (injection successful) ❌
```

**Recommendation:**
- Review all database queries for parameterization
- Implement input validation library (e.g., express-validator)
- Add Web Application Firewall (AWS WAF) with SQL injection rules

---

### A04:2021 - Insecure Design

**Description:** Missing or ineffective control design (threat modeling, secure design patterns).

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| No threat modeling conducted | ❌ Failed | ID.RA-01 | Payment flow not analyzed for threats | Conduct STRIDE analysis |
| Rate limiting not implemented | ❌ Failed | - | Can brute-force login (1000 req/min) | Implement rate limiting (5 attempts/min) |
| No account lockout policy | ❌ Failed | PR.AC-01 | Unlimited failed login attempts | Lock account after 5 failed attempts |

**Test Case:**
```bash
# Brute force test
for i in {1..1000}; do
  curl -X POST https://secureshop.com/api/login \
    -d "username=admin&password=test$i"
done
# All 1000 requests processed, no rate limiting ❌
```

**Recommendation:**
- Conduct STRIDE threat modeling for payment, authentication, and data access flows
- Implement rate limiting using AWS WAF or express-rate-limit
- Add account lockout after 5 failed attempts (15-minute lockout)

---

### A05:2021 - Security Misconfiguration

**Description:** Missing security hardening, unnecessary features enabled, default credentials.

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| Default admin credentials | ❌ **CRITICAL** | - | admin/admin123 works | Force password change on first login |
| Directory listing enabled | ❌ Failed | - | /uploads/ shows all files | Disable directory listing |
| Verbose error messages | ❌ Failed | - | Stack traces exposed to users | Implement generic error responses |
| Security headers missing | ❌ Failed | - | No CSP, X-Frame-Options, HSTS | Add security headers |

**Test Case:**
```bash
# Default credentials test
curl -X POST https://secureshop.com/api/login \
  -d "username=admin&password=admin123"
# Login successful ❌

# Directory listing test
curl https://secureshop.com/uploads/
# Returns HTML directory listing ❌

# Error disclosure test
curl https://secureshop.com/api/invalid
# Returns: "Error: Cannot read property 'id' of undefined
#  at getUserProfile (/app/server.js:45:12)" ❌
```

**Recommendation:**
- Rotate all default credentials immediately
- Apply CIS Benchmarks for OS and application hardening
- Implement custom error pages (no stack traces in production)
- Add security headers: Content-Security-Policy, X-Frame-Options, HSTS

---

### A07:2021 - Identification and Authentication Failures

**Description:** Weak authentication, session management flaws, credential stuffing vulnerabilities.

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| No MFA for admins | ❌ **CRITICAL** | PR.AC-01 | Single-factor authentication only | Deploy Okta MFA |
| Weak password policy | ❌ Failed | - | Allows "password123" | Enforce 12+ chars, complexity, no common passwords |
| Session fixation possible | ❌ Failed | - | Session ID not rotated on login | Regenerate session ID after login |
| Predictable session IDs | ⚠️ Warning | - | Sequential session IDs observed | Use cryptographically random tokens |

**Test Case:**
```bash
# Weak password test
curl -X POST https://secureshop.com/api/register \
  -d "username=test&password=123"
# Account created successfully ❌

# Session fixation test
# 1. Attacker gets session ID: SESS=abc123
# 2. Victim logs in with SESS=abc123
# 3. Attacker has authenticated session ❌
```

**Recommendation:**
- **Priority 1:** Deploy MFA for all admin accounts (Okta, Azure AD)
- Enforce strong password policy: 12+ chars, upper/lower/number/symbol, no common passwords
- Regenerate session ID after successful login
- Implement CAPTCHA after 3 failed login attempts

---

### A08:2021 - Software and Data Integrity Failures

**Description:** Insecure CI/CD pipelines, unsigned updates, compromised dependencies.

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| No dependency vulnerability scanning | ❌ Failed | PR.PT-02 | Using packages with known CVEs | Integrate Snyk/Dependabot |
| No code signing | ❌ Failed | - | Deployment artifacts unsigned | Implement code signing |
| CI/CD pipeline lacks security checks | ❌ Failed | - | No SAST/DAST in pipeline | Add SonarQube, OWASP ZAP |

**Test Case:**
```bash
# Check for vulnerable dependencies
npm audit
# Found 8 high severity vulnerabilities ❌

# Check package-lock.json
grep "lodash.*4.17.15" package-lock.json
# Lodash 4.17.15 has prototype pollution vulnerability ❌
```

**Recommendation:**
- Integrate Snyk into CI/CD pipeline (fail build on high/critical CVEs)
- Enable GitHub Dependabot alerts
- Add SAST (SonarQube) and DAST (OWASP ZAP) to pipeline
- Implement artifact signing in deployment process

---

### A09:2021 - Security Logging and Monitoring Failures

**Description:** Insufficient logging, no monitoring, delayed incident detection.

| Finding | Status | Associated Risk | Test Result | Remediation |
|---------|--------|-----------------|-------------|-------------|
| No centralized logging | ❌ Failed | DE.CM-01 | Logs scattered across instances | Deploy SIEM (AWS Security Hub) |
| Sensitive data in logs | ❌ Failed | - | Passwords logged in plaintext | Implement log sanitization |
| No alerting on suspicious events | ❌ Failed | DE.CM-01 | No alerts for failed logins, admin access | Configure CloudWatch alarms |
| Log retention too short | ⚠️ Warning | - | Only 7 days retained | Extend to 1 year (compliance requirement) |

**Test Case:**
```bash
# Check application logs
grep "password" /var/log/secureshop/app.log
# 2026-01-20 10:15:32 [INFO] Login attempt: user=admin, password=MyP@ssw0rd ❌

# Check for centralized logging
aws logs describe-log-groups
# No CloudWatch log groups configured ❌
```

**Recommendation:**
- Deploy AWS Security Hub + CloudWatch Logs for centralized logging
- Implement log sanitization (never log passwords, tokens, PII)
- Configure alerts for: 5+ failed logins, admin access, privilege escalation
- Extend log retention to 1 year (GDPR/PCI requirement)

---

### OWASP Top 10 Summary

| Risk | Status | Severity | Priority | Remediation Timeline |
|------|--------|----------|----------|---------------------|
| A01: Broken Access Control | ⚠️ Partial | HIGH | P2 | 30-60 days |
| A02: Cryptographic Failures | ❌ **CRITICAL** | CRITICAL | P1 | 0-30 days |
| A03: Injection | ⚠️ Partial | MEDIUM | P2 | 30-60 days |
| A04: Insecure Design | ❌ Failed | HIGH | P1 | 0-30 days |
| A05: Security Misconfiguration | ❌ Failed | HIGH | P2 | 30-60 days |
| A06: Vulnerable Components | ❌ Failed | MEDIUM | P3 | 60-90 days |
| A07: Auth Failures | ❌ **CRITICAL** | CRITICAL | P1 | 0-30 days |
| A08: Data Integrity | ❌ Failed | MEDIUM | P3 | 60-90 days |
| A09: Logging Failures | ❌ Failed | HIGH | P2 | 30-60 days |
| A10: SSRF | ✅ Pass | LOW | - | Monitoring only |

**Overall OWASP Coverage: 40%**  
**Critical Gaps: 2** (Cryptographic Failures, Auth Failures)  
**High Gaps: 4**

---

## 4. Cross-Framework Control Mapping

This section maps identified risks to multiple frameworks simultaneously to show control overlap.

| Risk ID | NIST CSF | PCI-DSS | GDPR | OWASP | ISO 27001 |
|---------|----------|---------|------|-------|-----------|
| PR.DS-01 | PR.DS-1 | Req 3.4 | Art 32 | A02 | A.8.2.3 |
| PR.AC-01 | PR.AC-6 | Req 8.3 | Art 32 | A07 | A.9.4.2 |
| DE.CM-01 | DE.CM-1 | Req 10.2 | Art 32 | A09 | A.12.4.1 |
| RS.CO-01 | RS.CO-1 | Req 12.10 | Art 33 | - | A.16.1.1 |
| PR.DS-04 | PR.DS-1 | Req 3.4 | Art 32 | A02 | A.10.1.1 |

**Key Insight:** Fixing PR.DS-01 (eliminate cardholder data) addresses:
- NIST CSF PR.DS-1 (data-at-rest protection)
- PCI-DSS Requirement 3.4 (render PAN unreadable)
- GDPR Article 32 (security of processing)
- OWASP A02 (cryptographic failures)
- ISO 27001 A.8.2.3 (protection of media)

**ROI:** Single control implementation achieves compliance across 5 frameworks

---

## 5. Remediation Investment Summary

### Investment by Framework

| Framework | Critical Gaps | Investment | Timeline | ROI |
|-----------|---------------|------------|----------|-----|
| PCI-DSS | 3 | $65,000 | 6-9 months | Enables payment processing |
| GDPR | 1 | $35,000 | 4-6 months | Avoids €20M fines |
| OWASP | 2 | $25,000 | 3-6 months | Reduces breach risk 75% |
| **Total** | **6** | **$125,000** | **9 months** | **$450K annual risk reduction** |

### Shared Controls (Cost Optimization)

Many controls satisfy multiple frameworks:

| Control | Cost | Frameworks Addressed |
|---------|------|---------------------|
| Tokenization | $15K | PCI-DSS (Req 3.4), GDPR (Art 32), OWASP (A02) |
| MFA Deployment | $5K | PCI-DSS (Req 8.3), GDPR (Art 32), OWASP (A07) |
| SIEM Solution | $12K/yr | PCI-DSS (Req 10), GDPR (Art 32), OWASP (A09), NIST (DE.CM) |
| Data Retention Policy | $8K | GDPR (Art 5), PCI-DSS (Req 3), NIST (PR.DS) |

**Cost Savings:** By implementing shared controls, total cost is $93K instead of $125K (26% savings)

---

## 6. Compliance Roadmap

### Phase 1: Critical Compliance (0-30 days) - $31K

**Goal:** Address blocking issues preventing payment processing and mitigate GDPR fine risk

| Action | Frameworks | Cost | Owner |
|--------|------------|------|-------|
| Implement payment tokenization | PCI 3.4, GDPR 32, OWASP A02 | $15K | Security Lead |
| Deploy MFA on admin accounts | PCI 8.3, GDPR 32, OWASP A07 | $5K | IAM Lead |
| Develop incident response plan | PCI 12.10, GDPR 33 | $5K | Security Lead |
| Create breach notification procedure | GDPR 33 | $3K | Legal/Compliance |
| Implement data classification | NIST ID.AM, PCI 3.1 | $3K | Security Lead |

**Deliverables:**
- ✓ Cardholder data eliminated from database
- ✓ MFA enabled for all admin accounts
- ✓ IR plan documented and socialized
- ✓ Breach notification templates created
- ✓ Data classified (public, internal, confidential, restricted)

---

### Phase 2: High-Priority Controls (30-90 days) - $37K

**Goal:** Implement detection and protective controls to achieve 70% compliance

| Action | Frameworks | Cost | Owner |
|--------|------------|------|-------|
| Deploy SIEM (AWS Security Hub) | PCI 10.2, GDPR 32, OWASP A09 | $12K/yr | SOC Lead |
| Implement WAF (AWS WAF) | PCI 6.4, OWASP A01/A03/A05 | $8K/yr | Network Lead |
| Enable database encryption | PCI 3.4, GDPR 32, OWASP A02 | $2K | DBA Lead |
| Implement data retention policy | GDPR 5(1)(e), PCI 3.1 | $8K | Legal/IT |
| Conduct Privacy Impact Assessment | GDPR 25 | $7K | Privacy Lead |

**Deliverables:**
- ✓ Centralized logging and alerting operational
- ✓ WAF protecting all public-facing applications
- ✓ Database encryption enabled (TDE)
- ✓ Automated data deletion after 7 years
- ✓ PIA completed for high-risk processing

---

### Phase 3: Comprehensive Compliance (90-180 days) - $25K

**Goal:** Achieve 90%+ compliance across all frameworks

| Action | Frameworks | Cost | Owner |
|--------|------------|------|-------|
| Implement vulnerability scanning | PCI 11.2, OWASP A08 | $6K/yr | SecOps Lead |
| Deploy EDR solution | PCI 5.2, GDPR 32 | $15K/yr | Security Lead |
| Establish third-party risk program | GDPR 28, PCI 12.8 | $4K | Procurement |
| Conduct penetration testing | PCI 11.3, OWASP (all) | $15K | Security Lead |
| Implement SAST/DAST in CI/CD | OWASP A08, PCI 6.3 | $10K | DevOps Lead |

**Deliverables:**
- ✓ Quarterly vulnerability scans operational
- ✓ Endpoint protection deployed to all systems
- ✓ Vendor security assessments completed
- ✓ Annual penetration test completed
- ✓ Security testing integrated into SDLC

---

## Conclusion

**Current State:** 15% PCI-DSS, 20% GDPR, 40% OWASP compliant  
**Target State:** 100% PCI-DSS, 95% GDPR, 90% OWASP compliant  
**Timeline:** 6-9 months  
**Investment:** $93,000  
**Risk Reduction:** $450,000/year → $75,000/year (83% reduction)  
**ROI:** 383%

**Critical Path:**
1. Month 1: Tokenization, MFA, IR Plan → Unblock payment processing
2. Months 2-3: SIEM, WAF, Encryption → Achieve detection and protection
3. Months 4-6: Scanning, Testing, Policies → Comprehensive compliance
4. Months 7-9: Remediation, QSA assessment, Certification

**Next Steps:**
1. Executive approval of $93K budget
2. Assign project owners for each phase
3. Kick off Phase 1 (tokenization project)
4. Schedule monthly compliance steering committee

---

**Prepared by:** Jeffin Sam Joji  
**Date:** January 25, 2026  
**Reviewed by:** [Security Lead, Legal, Executive Sponsor]
