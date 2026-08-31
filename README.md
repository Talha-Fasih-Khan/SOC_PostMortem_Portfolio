# SOC Post-Mortem Portfolio: Executive Summary

**Author:** Talha Khan  
**Role:** Junior SOC Analyst  
**Scope:** 460 Security Post-Mortem Reports  
**Objective:** Categorize, triage, and provide actionable intelligence on a large volume of endpoint detection alerts to demonstrate analytical maturity and environmental awareness.

---

## 1. The Challenge

SOC analysts are often overwhelmed by alert volume. The difference between a good analyst and a great one is the ability to **separate signal from noise** and **understand environmental context**. This portfolio represents a deep-dive analysis of 460 real-world security alerts, spanning Trojans, remote administration tools (RMMs), Potentially Unwanted Applications (PUAs), and ubiquitous false positives.

---

## 2. The Analysis Methodology

Each report was evaluated against the following framework to ensure consistency and actionable outcomes:

- **What:** Identification of the specific file, process, and threat classification.
- **Where:** Analysis of file paths, device context, and network location.
- **Why:** Determination of the root cause—was this user error, malicious intent, sanctioned IT activity, or environmental noise?
- **Verdict:** Classification into one of four threat-based categories:
  - 🔴 `01_Malware_Infections` – True positives requiring immediate remediation.
  - 🔵 `02_DualUse_Admin_Tools` – Legitimate tools (RMMs, VPNs, SSH) flagged due to dual-use potential.
  - 🟣 `03_PUA_Riskware` – Policy violations (crypto miners, adware, browser hijackers).
  - ⚪ `04_FalsePositives_Benign` – Completely clean system components or applications.

---

## 3. High-Level Findings & Statistics

| Category | Count | Percentage | Implication |
| :--- | :--- | :--- | :--- |
| **False Positives (Benign)** | 280 | **60.9%** | The overwhelming majority of alerts were environmental noise, highlighting a significant opportunity for EDR tuning. |
| **Dual-Use / Admin Tools** | 146 | **31.7%** | Nearly a third of alerts came from sanctioned RMMs (Splashtop, ScreenConnect, Syncro) used by our MSP, demonstrating the need for context-aware triage. |
| **PUA / Riskware** | 25 | 5.4% | Unauthorized software (crypto miners, adware toolbars) violated policy but were not indicative of advanced persistent threats. |
| **True Malware** | 9 | 2.0% | Only a fraction of alerts represented genuine threats, including Trojans, droppers, and phishing attempts. |

---

## 4. Key Strategic Takeaways & Recommendations

### 4.1. Tuning Opportunity (The "Dell SARemediation" Problem)
**Discovery:** Over 150 alerts were generated solely by the Dell SupportAssist Remediation backup folder (`C:\ProgramData\Dell\SARemediation\SystemRepair\Snapshots\Backup\*`). This folder contains recovery copies of legitimate Windows BitLocker and Sysinternals files.

**Recommendation:** Add a permanent exclusion for this path in the EDR policy.
> **Impact:** This single change would reduce total alert volume by **~33%**, freeing up SOC resources to focus on genuine threats.

### 4.2. Contextual Triage (The "MSP RMM" Problem)
**Discovery:** A managed service provider (one of our clients) heavily utilizes Splashtop, ScreenConnect, Syncro, and RemotePC for legitimate remote support. These tools accounted for over 140 events.

**Recommendation:** Whitelist the legitimate installation paths for these RMMs.
> **Impact:** This eliminates "noise" alerts without compromising security, as new or unauthorized RMM installations would still generate alerts.

### 4.3. User Education (The "PUA" Problem)
**Discovery:** A significant number of PUAs (crypto miners, Wave/Pulse Browser, PC App Store) were installed either unintentionally or via software bundling.

**Recommendation:** Reinforce user awareness training regarding downloading software from unverified sources and monitoring for unexpected browser toolbars.

---

## 5. Value to the Organization

This analysis demonstrates the ability to:

1.  **Reduce Alert Fatigue:** By identifying massive noise clusters and proposing whitelists, I provide a clear path to drastically lowering false positives.
2.  **Understand IT Environments:** I recognized that our IT ecosystem utilizes various RMMs and administrative tools—understanding this context prevents wasted time on benign activity.
3.  **Identify Real Threats:** Despite the noise, I successfully identified and documented 9 malicious incidents, including Trojans distributed via fake PDF editors and droppers, ensuring they were properly remediated.

---

## 6. Repository Structure

This portfolio is organized to demonstrate both **depth** (individual incident write-ups) and **breadth** (cluster summaries).

```text
📁 SOC_PostMortem_Portfolio/
├── 📁 01_Malware_Infections/     # 9 True Positives (Trojans, Droppers, Phishing)
├── 📁 02_DualUse_Admin_Tools/    # 146 events (RMMs, SSH, VPNs, BitLocker)
├── 📁 03_PUA_Riskware/           # 25 events (Miners, Adware, Toolbars)
├── 📁 04_FalsePositives_Benign/  # 280 events (Environmental Noise, System Processes)
└── README.md                     # This Executive Summary
