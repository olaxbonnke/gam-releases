# Privacy Policy for Gas Accounting Manager (GAM)

**Effective Date:** September 22, 2026  
**Last Updated:** September 22, 2026  
**Software:** GAM — Gas Accounting Manager (Desktop Application)  
**Publisher:** Olaitan / GAM Software Systems  

---

## 1. Introduction & Core Privacy Philosophy

Your privacy and the security of your business operations are paramount. **GAM (Gas Accounting Manager)** is intentionally engineered as an **offline-first, on-premise desktop application**. 

Unlike web-based point-of-sale systems that transmit sensitive revenue, customer phone numbers, and operational records to cloud servers, GAM stores and processes all business data **locally on your station's computer hardware**. 

We do **not** sell, monetize, track, mine, or share your business data with third parties or advertisers.

---

## 2. Information We Process Locally on Your Device

All information entered into GAM is stored in an embedded, local SQLite database (`pos.db`) residing on the station computer. This information includes:

### A. Operational & Sales Data
- Sales transactions, fuel weights (kg), itemized amounts, payment methods (Cash, Card, Transfer), and timestamp sequences.
- Customer names and contact telephone numbers entered optionally during ticket creation.
- Inter-branch transfer waybills, driver names, and vehicle registration numbers.

### B. Inventory & Plant Records
- Bulk Liquefied Petroleum Gas (LPG) storage pool levels and tank calibration entries.
- Tanker delivery intake manifests, purchase invoices, and supplier details.
- Retail accessory inventories (cylinders, burners, regulators, hoses) and unit pricing.

### C. Cashier & Financial Records
- Station expenses, expense descriptions, payment channels, and authorized staff signatures.
- Daily shift close sheets, expected cash calculations, physical drawer tallies, and cash discrepancies.
- User accounts (full name, username, assigned station role, and cryptographically salted password hashes).

**None of this operational data is ever transmitted to Olaitan, GAM Software Systems, or any external analytics platform.**

---

## 3. Hardware & Local System Device Access

To provide complete point-of-sale functionality, GAM accesses specific local hardware interfaces with your permission:

1. **Thermal Receipt Printers (USB / Network / Spooler)**:  
   GAM generates raw ESC/POS binary buffers to print customer receipts, shift close manifests, and waybills directly to attached 80mm thermal receipt printers. No printer telemetry or document content leaves the local network or computer.
2. **Removable Media (USB Flash Drives)**:  
   GAM can export verified snapshot backups and maintain automated secondary database mirrors on inserted USB drives. This process operates strictly on your local physical drives to prevent data loss in the event of workstation hardware failure.

---

## 4. Network Communications & Auto-Updates

GAM is engineered to function completely without an active internet connection. When an internet connection is present on the workstation, network communication is strictly limited to the following:

- **Checking for Official Software Updates**:  
  GAM queries our public GitHub distribution repository (`olaxbonnke/gam-releases`) to check if a newer version of the software is available.
- **Differential Patch Download**:  
  When an update is detected, GAM downloads the encrypted differential binary patch files (`GAM-Setup-<version>.exe`, `latest.yml`, `.blockmap`) directly from the secure GitHub CDN.
- **Zero Telemetry Transmitted**:  
  During update checks, **no sales figures, financial totals, customer contacts, or business records are sent**. The only data communicated to the distribution server is standard HTTPS request metadata (operating system type and current software version number) necessary to retrieve the correct installer package.

---

## 5. Staff Authentication & Data Security

We implement rigorous technical safeguards to secure station records:

- **Local Password Hashing**: All user passwords are encrypted using one-way salted `bcrypt` algorithms before saving to the local database. Plaintext passwords are never stored.
- **Process Isolation**: The user interface runs within a sandboxed Electron renderer using strict `contextIsolation` and disabled `nodeIntegration`, preventing untrusted scripts from accessing workstation files.
- **Transactional Database Safety**: The local SQLite database operates in Write-Ahead Logging (`WAL`) mode with atomic commits, preventing record corruption during unexpected power outages.
- **Physical Access Control**: Because data resides locally on the station computer, station owners are advised to maintain physical security of the terminal hardware, enable Windows account passwords, and store USB disaster recovery backups in a secure location.

---

## 6. Data Ownership, Retention & Deletion

- **Complete Data Sovereignty**: You own 100% of your business data. We claim zero proprietary interest in your sales records or operational metrics.
- **Data Export & Migration**: You can export your complete verified database backup snapshot at any time with a single click in the Settings or Setup screen.
- **Data Deletion**: Station owners have full authority to reset plant records, purge historical sales tickets, or permanently delete the local `pos.db` database from the workstation at their discretion.

---

## 7. Third-Party Services & Links

GAM does not embed third-party advertising networks, analytics trackers (such as Google Analytics or telemetry trackers), or third-party behavioral cookies. The application may contain optional direct support links (such as WhatsApp Customer Care), which, when clicked, open in your default web browser according to that third party's independent privacy policy.

---

## 8. Changes to This Privacy Policy

We may periodically update this Privacy Policy to reflect enhancements in the software or regulatory standards. When updates occur, the updated policy will be distributed with new releases of GAM and published in the application repository with a revised "Last Updated" date.

---

## 9. Contact Us

If you have questions regarding this Privacy Policy, your data sovereignty, or data protection practices in GAM, please contact:

- **Lead Developer**: Olaitan ([@olaxbonnke](https://github.com/olaxbonnke))
- **WhatsApp Support**: [https://wa.me/message/BFSG3COETP6IP1](https://wa.me/message/BFSG3COETP6IP1)
- **Project Repository**: [https://github.com/olaxbonnke/gam](https://github.com/olaxbonnke/gam)
