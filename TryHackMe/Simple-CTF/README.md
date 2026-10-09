# TryHackMe — Simple CTF

A beginner-level penetration testing assessment completed in the authorized **TryHackMe Simple CTF** lab. This project documents the assessment methodology, security weaknesses identified, and practical recommendations for improving Linux system security.

> **Ethical Disclaimer:** This assessment was performed in an authorized training environment. The purpose of this project is educational. Do not test systems without explicit permission. Passwords and challenge flags are not published in this repository.

## 📌 Project Overview

| Category                | Details                                                                             |
| ----------------------- | ----------------------------------------------------------------------------------- |
| Platform                | TryHackMe                                                                           |
| Lab                     | Simple CTF                                                                          |
| Difficulty              | Easy                                                                                |
| Assessment Type         | CTF / Penetration Testing Lab                                                       |
| Target Operating System | Linux                                                                               |
| Primary Focus           | Service Enumeration and Privilege Escalation                                        |
| Report                  | (./TryHackMe%20%E2%80%93%20Simple%20CTF%20Penetration%20Testing%20Report.pdf)       |

## 🎯 Objectives

* Identify exposed network services and their versions.
* Assess FTP access controls and publicly accessible files.
* Understand the risks of weak or reused passwords.
* Review SSH access and Linux user permissions.
* Identify privilege-escalation risks caused by excessive sudo permissions.
* Document security findings and recommend mitigations.

## 🛠️ Tools Used

| Tool           | Purpose                                            |
| -------------- | -------------------------------------------------- |
| Nmap           | Network and service enumeration                    |
| FTP Client     | Review FTP access and accessible files             |
| Hydra          | Authorized password-security testing in the lab    |
| SSH            | Remote access to the lab machine                   |
| GTFOBins       | Research risks associated with privileged binaries |
| Linux Commands | Review permissions and verify lab findings         |

## 🔍 Methodology

The assessment followed a structured penetration testing workflow.

### 1. Network Enumeration

**Objective:** Identify open ports and running services.

Nmap service detection was used to examine the authorized lab target.

```bash
nmap -sV <TARGET_IP>
```

The recorded lab results identified the following services:

| Port     | Service | Reported Version    |
| -------- | ------- | ------------------- |
| 21/tcp   | FTP     | vsftpd 3.0.3        |
| 80/tcp   | HTTP    | Apache httpd 2.4.18 |
| 2222/tcp | SSH     | OpenSSH 7.2p2       |

**Finding:** FTP, HTTP, and SSH services were accessible on the lab machine.

**Recommendation:** Disable unnecessary services, restrict network access, and keep exposed software updated.

### 2. FTP Enumeration

**Objective:** Review FTP access controls and identify accessible files.

The lab investigation identified anonymous FTP access and a file named `ForMitch.txt`, which contained a clue related to password reuse.

**Finding:** Information accessible through FTP provided useful clues for the lab investigation.

**Recommendations:**

* Disable anonymous FTP access unless explicitly required.
* Restrict access to files and directories.
* Remove sensitive information from publicly accessible locations.
* Prefer secure file-transfer protocols where appropriate.

### 3. Credential Security Assessment

**Objective:** Understand the risks associated with weak or reused passwords.

Password-security testing was conducted within the authorized TryHackMe lab environment.

**Finding:** The exercise demonstrated how weak credentials can compromise SSH account security.

**Recommendations:**

* Enforce strong, unique passwords.
* Use multi-factor authentication where supported.
* Apply appropriate authentication rate limits.
* Monitor repeated failed login attempts.
* Never publish passwords or recovered credentials.

### 4. Initial Access and Privilege Enumeration

**Objective:** Review the permissions available to the lab user.

After authorized access to the lab machine, sudo permissions were reviewed using:

```bash
sudo -l
```

The recorded lab configuration permitted the user `mitch` to run Vim as root without a password.

```text
(root) NOPASSWD: /usr/bin/vim
```

**Finding:** Allowing an interactive editor to run with root privileges can create a privilege-escalation risk.

**Recommendations:**

* Apply the principle of least privilege.
* Remove unnecessary passwordless sudo permissions.
* Avoid unrestricted privileged access to editors and shells.
* Audit sudoers configurations regularly.

### 5. Privilege-Escalation Analysis

GTFOBins was consulted to understand the security implications of allowing Vim to execute with elevated privileges.

**Finding:** The sudo configuration made Vim a potential route to root-level command execution.

**Potential Impact:** A user with this permission may be able to obtain administrative privileges beyond their intended access.

**Recommendations:**

* Remove unnecessary privileged editor permissions.
* Restrict sudo rules to specific administrative tasks.
* Review privileged binaries and their security implications.
* Validate permissions after applying remediation.

## ⚠️ Key Findings

| No. | Finding                                 | Indicative Risk | Recommended Mitigation                                   |
| --- | --------------------------------------- | --------------- | -------------------------------------------------------- |
| 1   | Anonymous FTP access                    | Medium          | Disable anonymous access if unnecessary                  |
| 2   | Information exposed through FTP         | Medium          | Restrict file access and remove sensitive information    |
| 3   | Weak or reused credentials              | High            | Enforce strong passwords and MFA                         |
| 4   | Excessive passwordless sudo permissions | Critical        | Apply least privilege and remove unnecessary permissions |
| 5   | Privileged Vim execution                | Critical        | Restrict editor execution with elevated privileges       |

*Risk ratings are preliminary qualitative assessments for this lab scenario, not formal CVSS scores. Actual severity depends on exposure, exploitability, and potential impact.*

## 🛡️ Security Recommendations

1. **Secure FTP:** Disable anonymous access when it is not required.
2. **Protect Sensitive Information:** Avoid storing credentials or sensitive hints in accessible directories.
3. **Strengthen Authentication:** Enforce unique passwords and multi-factor authentication where available.
4. **Apply Least Privilege:** Give users only the permissions required for their responsibilities.
5. **Audit Sudo Rules:** Review passwordless permissions and privileged executable access.
6. **Monitor Systems:** Track authentication failures and suspicious administrative activity.
7. **Maintain Software:** Apply security updates and review service configurations regularly.

## 📚 Skills Demonstrated

* Network service enumeration
* FTP access-control assessment
* SSH authentication security
* Linux permission analysis
* Sudo configuration review
* Privilege-escalation risk identification
* Security findings and remediation documentation

## 📄 Detailed Report

The complete penetration testing report can be added to this directory:

`TryHackMe-Simple-CTF-Penetration-Testing-Report.pdf`

**Note:** Upload the PDF using this exact filename for the link below to work.

 [📄 View Full Penetration Testing Report](./TryHackMe%20%E2%80%93%20Simple%20CTF%20Penetration%20Testing%20Report.pdf)


## ✅ Conclusion

The Simple CTF lab demonstrates how exposed services, accessible information, weak authentication, and excessive sudo permissions can combine to create serious security risks.

This practical strengthened my understanding of network enumeration, Linux permissions, authentication security, privilege-escalation analysis, and security documentation.

The key lesson is that secure configuration, strong authentication, and least-privilege access controls are essential for protecting Linux systems.

## 👨‍💻 Author

**Sunil Vaishnav**
Cybersecurity Student

**Areas of Learning**

* Cybersecurity
* Penetration Testing
* Linux Security
* Network Security
* AWS Cloud Security

---

*This project is intended for educational purposes and documents an authorized training lab. No credentials or challenge flags are intentionally disclosed.*

