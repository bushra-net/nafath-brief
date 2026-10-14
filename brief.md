Version: NAFATH-V4
Track: Software

## Overview

A national service provider depends on software, AI models, mobile applications, internet routing, cybersecurity practices, and reliable data records. These areas must work together because a weakness in one can affect the whole service. Software configuration must keep secrets outside source code, while AI systems need protection against poisoned training data and manipulated inputs. Mobile apps should be tested against a recognized security standard. Network operators can use RPKI route-origin validation to reduce some BGP hijacking risks, while understanding its limits. Security teams must identify and patch vulnerable components such as Log4j. Finally, a Software Bill of Materials helps teams identify which components are included in each release and respond when a dependency is affected. Together, these controls improve visibility, reduce preventable risk, and support safer service delivery. The Software track focuses on keeping configuration and secrets out of application code.

## Software

The Twelve-Factor App methodology says configuration that varies between deployments should be stored in environment variables, not hard-coded into the application. This includes service credentials, API keys, and database connection details. Keeping secrets out of source code reduces the chance that they will be exposed through a repository or copied into a release. Access to production secrets should still be restricted and managed securely.

Resource: The Twelve-Factor App: Config - https://12factor.net/config

## AI

Adversarial machine-learning attacks include evasion, poisoning, and privacy attacks. Evasion happens when an attacker changes an input to cause a model to make a wrong prediction. Poisoning happens when training data or the training process is manipulated so the model learns harmful behavior. Privacy attacks try to learn sensitive information about training data or model users. Defenses depend on the model and its lifecycle, so teams should assess risks before and after deployment.

Resource: Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations - https://csrc.nist.gov/pubs/ai/100/2/e2025/final

## Mobile

The OWASP Mobile Application Security Verification Standard (MASVS) defines security controls for mobile apps. Its control groups cover areas such as secure storage, cryptography, authentication, network communication, platform interaction, code quality, resilience, and privacy. A team uses MASVS to define what should be checked, then uses the OWASP Mobile Application Security Testing Guide (MASTG) for testing methods and test cases. Results help identify weaknesses and measure whether the app meets its security requirements.

Resource: OWASP MASVS - https://mas.owasp.org/MASVS/

## Networking

BGP route hijacking can occur when a network announces an IP prefix it is not authorized to originate, potentially attracting traffic away from its intended path. RPKI Route Origin Authorizations let networks check whether the originating autonomous system is authorized for a prefix. Route-origin validation can identify invalid announcements, and operators can apply routing policy to reject them. However, origin validation does not verify the complete AS path, so it cannot prevent every routing attack or misconfiguration.

Resource: RFC 6811: BGP Prefix Origin Validation - https://www.rfc-editor.org/info/rfc6811/

## Cybersecurity

Log4Shell (CVE-2021-44228) was a critical vulnerability in Apache Log4j 2. In affected versions, attacker-controlled input could trigger a JNDI lookup and potentially cause remote code execution, making the issue severe and widely relevant to applications that logged untrusted data. Apache listed fixed versions including 2.15.0 for Java 8 and later, with separate fixes for older Java versions. Organizations should identify affected deployments and upgrade to an appropriate supported fixed version.

Resource: Security - Apache Logging Services - https://logging.apache.org/security.html

## Data

A Software Bill of Materials (SBOM) is a structured inventory of software components and dependencies in a product. It helps teams understand what is included in a release and quickly check whether a vulnerable component is present. A useful SBOM identifies the document format and specification version and records component details such as name, version, supplier or author when known, and identifiers that help distinguish components. Teams should generate it consistently and keep it linked to the software release it describes.

Resource: CycloneDX Specification - https://github.com/CycloneDX/specification

## Misconception in My Track

A common misconception is that putting configuration in a separate file automatically keeps secrets safe. The Twelve-Factor App specifically recommends environment variables for deployment-specific configuration and explains that checked-in config files can still be accidentally committed and that scattered files are difficult to manage. This does not mean environment variables alone are a complete secrets-management system: access must still be controlled, and secrets should not be printed in logs or exposed to unauthorized processes. The relevant evidence is in the resource section titled â2. A twelve-factor app stores config in environment variables.â

## Open Question

How should the provider manage and rotate production secrets across its deployment platform while ensuring that applications, logs, and build pipelines do not expose them?
