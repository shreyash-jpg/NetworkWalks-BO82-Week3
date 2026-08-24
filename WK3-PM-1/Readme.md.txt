# PDF Password Recovery Tool using John the Ripper & Johnny GUI

A beginner-friendly demonstration and documentation of recovering passwords from encrypted PDF files using **John the Ripper (JTR)** and its graphical frontend **Johnny**.

---

## 📌 Overview

This repository demonstrates the step-by-step methodology for auditing and cracking password-protected PDF files in a security testing environment. The goal is to understand how hashes are extracted from document containers and processed using dictionary/incremental attacks to assess password strength.

---

## 🛠️ Tools Required

* **[John the Ripper (JTR)](https://www.openwall.com/john/)**: Core command-line password recovery tool.
* **[Johnny GUI](https://openwall.info/wiki/john/johnny)**: Graphical Interface for John the Ripper.
* **[OnlineHashCrack PDF Extractor](https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php)** *(or local `pdf2john.py` script)*: For extracting hash signatures from PDF files.

---

## 🚀 Step-by-Step Guide

### Step 1: Tool Installation & Configuration

1. **Download John the Ripper**: Extract the archive to a local directory (e.g., `C:\JohnTheRipper`).
2. **Install Johnny GUI**: Run the setup wizard and launch the application.
3. **Link JTR Engine**:
   * Navigate to **Settings** in Johnny.
   * Browse and select `john.exe` located inside the JTR `run/` directory.

### Step 2: Hash Extraction & Formatting

1. Upload the target file (`My Locked PDF1.pdf`) to the PDF Hash Extraction tool (or process locally via `pdf2john.py`).
2. Copy the resulting hash payload.
3. **Clean the Hash**: Ensure any language wrapper prefixes (e.g., Python `b'...'` formatting) are removed. The hash **must** start with the `$pdf$` signature.
   
   *Example clean hash format:*
   ```text
   $pdf$1*2*3*0*1*16*...