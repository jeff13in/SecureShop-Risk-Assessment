# E-Commerce Security Risk Assessment & Compliance Analysis Project

**Author:** Jeffin Sam Joji  
**Date:** January 2026  
**Duration:** 3 weeks  
**Frameworks:** NIST Cybersecurity Framework, PCI-DSS v4.0, GDPR, OWASP Top 10 (2021)

---

## Project Overview

This project demonstrates comprehensive Governance, Risk, and Compliance (GRC) capabilities through a security risk assessment of a hypothetical e-commerce platform ("SecureShop"). The assessment identifies 18 security control gaps, maps them to multiple compliance frameworks, develops Key Risk Indicators (KRIs), and creates a prioritized remediation roadmap.

### Business Impact

- **Risk Exposure Identified:** $450,000 annual loss expectancy
- **Compliance Gaps:** PCI-DSS (15%), GDPR (20%), OWASP (40%)
- **Remediation Investment:** $93,000 over 9 months
- **Expected Risk Reduction:** 83% (from $450K to $75K annually)
- **Return on Investment:** 383%

---

## Project Objectives

1. **Risk Assessment:** Conduct systematic risk analysis using NIST Cybersecurity Framework
2. **Compliance Mapping:** Map identified risks to PCI-DSS, GDPR, and OWASP Top 10 requirements
3. **KRI Development:** Create measurable Key Risk Indicators for ongoing monitoring
4. **Remediation Planning:** Develop prioritized, costed remediation roadmap

---

## Project Deliverables

### 1. SecureShop_Risk_Assessment.md
**Description:** Comprehensive security risk assessment document covering:
- Asset inventory and classification
- Risk analysis across 5 NIST CSF domains (Identify, Protect, Detect, Respond, Recover)
- 18 identified risks with likelihood, impact, and risk scores
- Control gap analysis
- Remediation recommendations with cost-benefit analysis

**Key Sections:**
- **Asset Inventory:** 6 critical assets classified by sensitivity
- **Risk Matrix:** 18 risks rated from Critical (score 20) to Medium (score 8)
- **Control Gaps:** Specific missing controls mapped to NIST CSF subcategories
- **KRIs:** 24 Key Risk Indicators across technical, compliance, and operational domains
- **Roadmap:** 3-phase remediation plan with timeline and costs

**How to Use:**
- Review Section 2 (Risk Assessment Matrix) for detailed risk analysis
- Use Section 5 (KRIs) to understand current risk posture
- Reference Section 6 (Remediation Roadmap) for prioritized action plan
- Share Executive Summary with business stakeholders for approval

---

### 2. SecureShop_KRI_Dashboard.xlsx
**Description:** Interactive Excel dashboard with 7 worksheets for risk monitoring and visualization.

**Worksheets:**

1. **Executive Dashboard**
   - Overall risk score (67/100 - High Risk)
   - Compliance status summary (PCI-DSS, GDPR, NIST CSF, OWASP)
   - Risk summary by severity (3 Critical, 9 High, 6 Medium)
   - Financial impact analysis ($450K current risk, $93K investment, 383% ROI)

2. **Technical KRIs**
   - 8 technical security indicators (patch management, vulnerability metrics, access control)
   - Target vs. current values with status (Red/Yellow/Green)
   - Trend analysis (increasing, declining, stable)

3. **Compliance KRIs**
   - 8 compliance metrics (PCI-DSS score, GDPR compliance, policy reviews)
   - Overdue findings and training completion rates

4. **Operational KRIs**
   - 8 operational metrics (MTTD, MTTR, backup success, DR testing)
   - Incident tracking and system uptime

5. **Risk Register**
   - Complete list of 15 identified risks
   - Risk ID, description, likelihood, impact, risk score, status, owner
   - Filterable and sortable for risk prioritization

6. **Trend Analysis**
   - 12-month trend data for 6 key KRIs
   - Visual line chart showing risk trajectory
   - Historical performance for executive reporting

7. **Remediation Roadmap**
   - Detailed remediation plan with 11 prioritized actions
   - Priority (P1/P2/P3), timeline, cost, owner, status, due date
   - Total investment summary ($93,000)

**How to Use:**
- Start with "Executive Dashboard" for high-level overview
- Use "Technical/Compliance/Operational KRIs" for detailed monitoring
- Reference "Risk Register" for specific risk details
- Track progress using "Remediation Roadmap" worksheet
- Share "Trend Analysis" charts in quarterly executive reviews
- Update KRI values monthly to track improvement

**Key Features:**
- Color-coded status indicators (Red = Critical/High, Yellow = Medium, Green = On-Track)
- Embedded formulas for automatic calculations
- Conditional formatting for visual risk identification
- Ready for monthly/quarterly reporting

---

### 3. Compliance_Mapping.md
**Description:** Detailed mapping of identified risks to regulatory requirements and industry standards.

**Key Sections:**

1. **PCI-DSS v4.0 Compliance Mapping**
   - Detailed analysis of 12 PCI-DSS requirements
   - Current compliance: 15% (3 Critical blockers)
   - Critical gaps: Storing cardholder data, No MFA, No IR plan
   - Requirement-by-requirement status with remediation steps
   - Estimated time to compliance: 6-9 months, Cost: $65,000

2. **GDPR Compliance Mapping**
   - Analysis of 7 GDPR articles (Art 5, 15-22, 25, 30, 32, 33, 44-49)
   - Current compliance: 20%
   - Critical gap: No breach notification procedure (Art 33 - 72-hour requirement)
   - Data subject rights implementation status
   - Fine exposure: Up to €20M or 4% of revenue
   - Estimated time to compliance: 4-6 months, Cost: $35,000

3. **OWASP Top 10 (2021) Coverage**
   - Analysis of all 10 OWASP risks with test cases
   - Current coverage: 40% (4 failed controls, 5 partial)
   - Critical gaps: Cryptographic Failures (A02), Authentication Failures (A07)
   - Specific vulnerability findings with proof-of-concept tests
   - Remediation timeline and costs

4. **Cross-Framework Control Mapping**
   - Shows how single controls satisfy multiple frameworks
   - Example: Tokenization addresses PCI 3.4, GDPR Art 32, OWASP A02, ISO 27001 A.8.2.3
   - Cost optimization through shared controls (26% savings)

5. **Remediation Investment Summary**
   - Investment by framework (PCI: $65K, GDPR: $35K, OWASP: $25K)
   - Shared controls reduce total cost from $125K to $93K
   - 6-month compliance roadmap

**How to Use:**
- Use PCI-DSS section to understand payment processing compliance gaps
- Reference GDPR section for data protection requirements
- Review OWASP section for application security priorities
- Share Cross-Framework Mapping with executives to show cost efficiency
- Use Remediation Investment Summary for budget planning

---

## Technical Approach

### Risk Assessment Methodology

1. **Asset Identification**
   - Cataloged 6 critical system components
   - Classified by data sensitivity and business criticality

2. **Threat Analysis**
   - Identified 18 distinct risks across NIST CSF domains
   - Used industry-standard likelihood and impact scoring (1-5 scale)
   - Calculated risk scores (Likelihood × Impact)

3. **Control Gap Analysis**
   - Compared current controls against NIST CSF baseline
   - Identified missing, partial, and failed controls
   - Documented specific remediation requirements

4. **Compliance Mapping**
   - Cross-referenced risks to PCI-DSS, GDPR, OWASP requirements
   - Identified overlapping controls across frameworks
   - Optimized remediation for multi-framework compliance

### KRI Development Methodology

**Selection Criteria:**
- **Measurable:** Quantifiable metrics with clear targets
- **Actionable:** Drive specific remediation decisions
- **Relevant:** Aligned to business objectives and compliance requirements
- **Timely:** Enable early warning before issues escalate

**KRI Categories:**
1. **Technical Security:** Patch management, vulnerability metrics, access control
2. **Compliance:** Framework adherence scores, policy reviews, audit findings
3. **Operational:** Incident response times, system availability, backup success
4. **Business Impact:** Financial loss expectancy, downtime incidents, regulatory fines

**Thresholds:**
- **Red (Critical):** Immediate action required, escalate to executives
- **Yellow (Warning):** Monitoring required, schedule remediation
- **Green (On-Track):** Meets target, maintain current controls

---

## Key Findings

### Critical Risks (Score 20 - Immediate Action Required)

1. **PR.DS-01: Storing Cardholder Data (PCI-DSS Violation)**
   - **Impact:** Cannot process payments, fines up to $100K/month
   - **Root Cause:** Full PAN stored in database instead of tokenization
   - **Remediation:** Implement payment gateway tokenization
   - **Cost:** $15,000 | **Timeline:** 30 days

2. **PR.AC-01: No Multi-Factor Authentication on Admin Accounts**
   - **Impact:** Account takeover via credential stuffing/phishing
   - **Root Cause:** Password-only authentication
   - **Remediation:** Deploy Okta/Azure AD MFA
   - **Cost:** $5,000 | **Timeline:** 30 days

3. **ID.RA-01: No Threat Modeling for Payment Flow**
   - **Impact:** Unknown vulnerabilities in critical payment processing
   - **Root Cause:** No security analysis in development lifecycle
   - **Remediation:** Conduct STRIDE threat modeling
   - **Cost:** $3,000 | **Timeline:** 30 days

### High Risks (Score 12-16 - Short-term Remediation)

- No SIEM solution (blind to security incidents)
- No WAF protection (OWASP Top 10 exposure)
- Database encryption disabled (data breach exposure)
- No incident response plan (ineffective breach response)
- Excessive database permissions (insider threat)

### Compliance Gaps

**PCI-DSS:** 15% compliant
- **Blockers:** Storing cardholder data, No MFA, No IR plan
- **Timeline to Compliance:** 6-9 months

**GDPR:** 20% compliant
- **Blockers:** No breach notification procedure, No data retention policy
- **Fine Risk:** Up to €20M or 4% of revenue

**OWASP Top 10:** 40% coverage
- **Blockers:** Cryptographic failures, Authentication failures
- **Breach Risk:** 75% reduction after remediation

---

## Remediation Roadmap

### Phase 1: Critical Compliance (0-30 Days) - $31,000

**Objective:** Unblock payment processing and mitigate regulatory fine risk

| Action | Frameworks Addressed | Cost | Owner |
|--------|---------------------|------|-------|
| Payment tokenization | PCI 3.4, GDPR 32, OWASP A02 | $15K | Security Lead |
| Deploy MFA | PCI 8.3, GDPR 32, OWASP A07 | $5K | IAM Lead |
| Develop IR plan | PCI 12.10, GDPR 33 | $5K | Security Lead |
| Breach notification procedure | GDPR 33 | $3K | Legal/Compliance |
| Data classification | NIST ID.AM, PCI 3.1 | $3K | Security Lead |

**Success Metrics:**
- ✓ Zero cardholder data in database
- ✓ 100% admin accounts with MFA
- ✓ IR plan documented and tested
- ✓ Breach notification templates approved by legal

---

### Phase 2: High-Priority Controls (30-90 Days) - $37,000

**Objective:** Implement detection and protection controls

| Action | Frameworks Addressed | Cost | Owner |
|--------|---------------------|------|-------|
| Deploy SIEM | PCI 10.2, GDPR 32, OWASP A09 | $12K/yr | SOC Lead |
| Implement WAF | PCI 6.4, OWASP A01/A03/A05 | $8K/yr | Network Lead |
| Enable database encryption | PCI 3.4, GDPR 32, OWASP A02 | $2K | DBA Lead |
| Data retention policy | GDPR 5(1)(e), PCI 3.1 | $8K | Legal/IT |
| Privacy Impact Assessment | GDPR 25 | $7K | Privacy Lead |

**Success Metrics:**
- ✓ SIEM monitoring 100% of infrastructure
- ✓ WAF blocking OWASP Top 10 attacks
- ✓ Database encryption enabled (TDE)
- ✓ Automated data deletion after 7 years

---

### Phase 3: Comprehensive Compliance (90-180 Days) - $25,000

**Objective:** Achieve 90%+ compliance across all frameworks

| Action | Frameworks Addressed | Cost | Owner |
|--------|---------------------|------|-------|
| Vulnerability scanning | PCI 11.2, OWASP A08 | $6K/yr | SecOps Lead |
| Deploy EDR | PCI 5.2, GDPR 32 | $15K/yr | Security Lead |
| Third-party risk program | GDPR 28, PCI 12.8 | $4K | Procurement |
| Penetration testing | PCI 11.3, OWASP (all) | $15K | Security Lead |
| SAST/DAST in CI/CD | OWASP A08, PCI 6.3 | $10K | DevOps Lead |

**Success Metrics:**
- ✓ Quarterly vulnerability scans operational
- ✓ Endpoint protection on 100% of systems
- ✓ Vendor security assessments completed
- ✓ Annual penetration test passed
- ✓ Security testing in SDLC (every build)

---

## Skills Demonstrated

This project showcases the following GRC and cybersecurity competencies:

### Governance, Risk & Compliance
- ✓ Risk assessment using industry frameworks (NIST CSF)
- ✓ Compliance gap analysis (PCI-DSS, GDPR, OWASP)
- ✓ Control mapping across multiple frameworks
- ✓ Key Risk Indicator (KRI) development and monitoring
- ✓ Regulatory requirement interpretation
- ✓ Remediation roadmap development with cost-benefit analysis

### Technical Security
- ✓ Vulnerability analysis and threat modeling
- ✓ Security control design and implementation planning
- ✓ SIEM, WAF, encryption, and access control solutions
- ✓ Application security (OWASP Top 10)
- ✓ Cloud security (AWS)
- ✓ Data protection and privacy controls

### Business & Communication
- ✓ Executive summary and stakeholder reporting
- ✓ Risk quantification and financial impact analysis
- ✓ Technical findings translated to business risk
- ✓ Prioritization based on business impact
- ✓ Budget planning and ROI justification
- ✓ Cross-functional collaboration (security, legal, IT, business)

### Tools & Methodologies
- ✓ NIST Cybersecurity Framework (CSF)
- ✓ PCI-DSS v4.0 compliance requirements
- ✓ GDPR regulatory analysis
- ✓ OWASP Top 10 application security
- ✓ ISO 27001 control mapping
- ✓ Risk matrices and heat maps
- ✓ Excel dashboards with KPIs/KRIs

---

## How to Present This Project

### Resume Bullet Points

**Risk Assessment & Compliance Analysis Project** | January 2026
- Conducted comprehensive security risk assessment on e-commerce platform using NIST Cybersecurity Framework, identifying 18 control gaps across 5 domains with quantified business impact ($450K annual loss exposure)
- Mapped security risks to PCI-DSS, GDPR, and OWASP Top 10 requirements, achieving compliance gap analysis across multiple regulatory frameworks with remediation cost optimization (26% savings through shared controls)
- Developed Key Risk Indicator (KRI) dashboard tracking 24 metrics across technical, compliance, and operational domains with automated status reporting (Red/Yellow/Green) for executive visibility
- Created prioritized remediation roadmap with 3-phase approach (0-30, 30-90, 90-180 days) and cost-benefit analysis, demonstrating 383% ROI through risk reduction from $450K to $75K annually
- Technologies: NIST CSF, PCI-DSS v4.0, GDPR, OWASP Top 10, ISO 27001, Excel (advanced formulas, pivot tables, dashboards), risk assessment methodologies

### Interview Talking Points

**Question: "Tell me about a time you conducted a risk assessment."**

"I conducted a comprehensive security risk assessment on a hypothetical e-commerce platform to demonstrate GRC capabilities. Using the NIST Cybersecurity Framework, I identified 18 control gaps across the five domains—Identify, Protect, Detect, Respond, and Recover.

I started by inventorying and classifying assets based on data sensitivity, then analyzed risks using a likelihood and impact matrix. For example, I found they were storing full cardholder data in their database, which is a PCI-DSS Requirement 3.4 violation with a risk score of 20 out of 20—critical severity.

I then mapped each risk to multiple compliance frameworks—PCI-DSS, GDPR, and OWASP Top 10—to show overlapping requirements. This allowed me to optimize remediation by implementing shared controls. For instance, tokenizing payment data addressed PCI compliance, GDPR Article 32 security requirements, and OWASP A02 cryptographic failures.

The deliverable was a detailed risk assessment document, an Excel KRI dashboard with 24 metrics, and a prioritized remediation roadmap with costs and timelines. I demonstrated that a $93,000 investment over 9 months could reduce annual risk exposure from $450,000 to $75,000—a 383% ROI."

---

**Question: "How do you prioritize security risks?"**

"I use a quantitative approach based on likelihood, impact, and business criticality. In my e-commerce risk assessment, I scored each risk on a 1-5 scale for likelihood and impact, then multiplied them to get a risk score.

Critical risks—like storing cardholder data and no MFA on admin accounts—scored 20 out of 20 because they had high likelihood of exploitation and critical business impact. These became Phase 1 priorities with 0-30 day timelines.

But I also considered compliance dependencies. For example, implementing payment tokenization was the highest priority not just because of the risk score, but because it was a PCI-DSS blocker preventing the company from processing payments. The regulatory penalty was $100,000 per month, so that became the immediate focus.

I also looked for control overlap. By implementing tokenization, we simultaneously addressed PCI-DSS Requirement 3.4, GDPR Article 32, and OWASP A02—three frameworks with one control. That cost optimization informed my prioritization."

---

**Question: "What Key Risk Indicators would you track for an e-commerce platform?"**

"I developed 24 KRIs across four categories:

**Technical Security KRIs:**
- Mean Time to Patch Critical Vulnerabilities: Target ≤7 days vs. Current 28 days
- Percentage of Assets with Current Patches: Target ≥95% vs. Current 68%
- Failed Admin Login Attempts: Target ≤10/day vs. Current 45/day

**Compliance KRIs:**
- PCI-DSS Compliance Score: Target 100% vs. Current 15%
- GDPR Compliance Score: Target 100% vs. Current 20%
- Overdue Compliance Findings: Target 0 vs. Current 18

**Operational KRIs:**
- Mean Time to Detect (MTTD): Target ≤4 hours vs. Current Unknown
- Mean Time to Respond (MTTR): Target ≤8 hours vs. Current Unknown
- Backup Success Rate: Target 100% vs. Current 94%

**Business Impact KRIs:**
- Estimated Annual Loss Expectancy: Target <$50K vs. Current $450K
- Security Incidents Causing Downtime: Target 0/quarter vs. Current 2/quarter

I built an Excel dashboard with color-coded status indicators—Red for critical, Yellow for warning, Green for on-track—and included 12-month trend analysis to show risk trajectory. This gave executives actionable visibility into security posture."

---

## Files in This Project

```
GRC_Project/
├── README.md                           # This file
├── SecureShop_Risk_Assessment.md       # Comprehensive risk assessment
├── SecureShop_KRI_Dashboard.xlsx       # Interactive KRI dashboard
└── Compliance_Mapping.md               # Detailed compliance analysis
```

---

## Next Steps

To further enhance this project for job applications:

1. **Create a 1-page Executive Summary**
   - Distill key findings into C-suite language
   - Emphasize ROI and business impact
   - Include visual risk heat map

2. **Build a PowerPoint Presentation**
   - 10-slide deck summarizing the assessment
   - Visual charts from KRI dashboard
   - Use for portfolio and interviews

3. **Add a Threat Modeling Diagram**
   - Create STRIDE analysis for payment flow
   - Visual data flow diagram showing attack vectors
   - Demonstrates application security expertise

4. **Optional: Implement a Control**
   - Actually deploy AWS WAF or configure MFA in a lab environment
   - Document the implementation
   - Shows hands-on technical capability

---

## Conclusion

This project demonstrates end-to-end GRC capabilities:
- **Risk Assessment:** Systematic analysis using industry frameworks
- **Compliance Analysis:** Multi-framework mapping with cost optimization
- **KRI Development:** Measurable indicators for ongoing monitoring
- **Business Communication:** Translating technical risks to financial impact
- **Remediation Planning:** Prioritized roadmap with timeline and budget

**Alignment with American Express Role:**
- Governance, Risk, Compliance (GRC) → Risk analysis, compliance mapping, KRI development
- Security Investigations → Risk identification, control gap analysis
- Regulatory Guidance → PCI-DSS, GDPR compliance expertise
- Communication Skills → Executive summaries, stakeholder reporting

**Total Effort:** ~20-25 hours over 3 weeks  
**Complexity Level:** Intermediate-Advanced GRC  
**Suitable for:** Entry-level to mid-level security analyst positions

---

**Contact:**
Jeffin Sam Joji  
ejffinsam14@gmail.com  
[LinkedIn](https://linkedin.com/in/jeffin-sam-joji) | [Portfolio](https://jeffinsam.com)
