# PDF Password Recovery Walkthrough (John the Ripper & Johnny GUI)

A comprehensive, step-by-step security testing guide for extracting and cracking password-protected PDF files using **John the Ripper (JTR)** and the **Johnny GUI** on Windows.

---

## 📌 Prerequisites

Before starting, ensure you have the following downloaded on your Windows PC:

* **Target File**: `My Locked PDF1.pdf`
* **John the Ripper (JTR)**: Core password cracking engine ([Openwall Official Download](https://www.openwall.com/john/))
* **Johnny GUI**: Graphical front-end interface ([Openwall Johnny Wiki](https://openwall.info/wiki/john/johnny))

---

## 📑 Detailed Walkthrough

### Phase 1: Environment Setup & Configuration

#### Step 1: Extract John the Ripper (JTR)
1. Download the JTR Windows binary package archive (e.g., `john-1.9.0-jumbo-1-win64.zip`).
2. Extract the ZIP package to an easily accessible location on your PC (e.g., `C:\JohnTheRipper`).
3. Locate the `run` folder inside the extracted directory (path: `C:\JohnTheRipper\run\`). This directory contains the `john.exe` core executable and various hash-extraction scripts.

#### Step 2: Install Johnny GUI
1. Run the downloaded installer executable for Johnny (e.g., `johnny-setup.exe`).
2. Follow the setup wizard prompts to complete installation and launch **Johnny**.

#### Step 3: Link Johnny to the JTR Core Engine
1. In the Johnny application window, click on the **Settings** tab located in the top navigation bar.
2. Under the **Path to John binary** field, click **Browse**.
3. Navigate to the `run` folder of your extracted JTR installation (`C:\JohnTheRipper\run\`).
4. Select `john.exe` and click **Open**.
5. Click **Save** or **Apply** to confirm the link.

---

### Phase 2: Hash Extraction & Formatting

Password cracking tools cannot process raw `.pdf` files directly; they require the cryptographic hash signature derived from the document's header.

#### Step 4: Extract the PDF Hash Signature
1. Open your web browser and navigate to an online extraction service, such as the [OnlineHashCrack PDF Hash Extractor](https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php).
2. Click **Browse** / **Choose File**, select `My Locked PDF1.pdf`, and click **Upload**.
3. Once processed, the website will output a raw cryptographic string representing the encrypted header. Copy the entire generated output string.

#### Step 5: Clean and Format the Hash String
1. Open **Notepad** (or any plain text editor).
2. Paste the copied hash string into the editor.
3. **Inspect the formatting**:
   * If the string contains a Python byte wrapper prefix like `b'$pdf$...'` or surrounding single quotes `'`, **delete the prefix `b'` and outer quotes**.
   * The hash line **must start directly with `$pdf$`** and contain no leading spaces or extra characters.
   
   *Correct format example:*
   ```text
   $pdf$1*2*3*0*1*16*a1b2c3d4e5f6...