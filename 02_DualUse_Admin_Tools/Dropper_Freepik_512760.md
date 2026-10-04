# Incident Report: Freepik AdWare

**Event ID:** 512760  
**Date/Time:** 07/15/2024 14:08:06  
**Investigator:** Talha Khan

---

## 1. Overview

  The user downloaded a platform of AI-powered creative tools that wound up being a generic Trojan that possibly installed adware onto their computer.

---

## 2. Triage Details

| Field | Detail |
| :--- | :--- |
| **User / Device** | Willy/WILL-NITRO5 |
| **OS** | Windows 11 Pro |
| **File Name** | `Freepik素材下载器.exe` |
| **File Path** | `D:\OneDrive - Huafan University\軟體\Freepik素材下载器.exe` |
| **Certificate Owner** | N/A, Not Signed |
| **Threat Type** | Adware / PUP/PUA / True Positive |

---

## 3. Root Cause Analysis

  The user intentionally or unintentionally downloaded some AI-powered software that was actually a Trojan.

---

## 4. Technical Evidence

- **Hash (SHA256):** `49a2fdf5b2b27b60b6ffd5e1f1e88f9065431ce7d294aa049cac61680e20442c`
- **VirusTotal Results:** [Link to VT](https://www.virustotal.com/gui/file/49a2fdf5b2b27b60b6ffd5e1f1e88f9065431ce7d294aa049cac61680e20442c/detection)
- **Behavior:** The executable (`Freepik素材下载器.exe`) attempted to install adware.
- Freepik: [Link](https://www.freepik.com/)
- Trojan.MalPack.FlyStudio: [Link](https://www.malwarebytes.com/blog/detections/trojan-malpack-flystudio)
- What is FileRepMalware and should you remove it?: [Link](https://www.expressvpn.com/blog/filerepmalware/)


---

## 5. Verdict

**Verdict:** `PUA` (True Positive)

---

## 6. Actions Taken / Recommendations

- [x] Contacted the user to confirm the download was unintentional.
- [x] Advised the user to delete the file and clear the Downloads folder.
- [x] Advised the user to restart the device and perform a full scan to confirm the absence of malware.
- [ ] Escalate to the security team if persistence is detected.

---

## 7. Tags
`#Trojan` `#PUA` `#UserError`

