# Comparative Security Guide: PDF Password Recovery Methods

A detailed breakdown comparing offline password recovery using **John the Ripper (JTR) & Johnny GUI** against browser-based extraction using **Networkwalks (NW) Web Tools**.

---

## 📊 Overview & Comparison

| Feature / Metric | John the Ripper (JTR) + Johnny GUI | Networkwalks (NW) Web Tools |
| :--- | :--- | :--- |
| **Execution Environment** | Local Machine (Offline) | Web Browser (Cloud/Remote) |
| **Prerequisites** | JTR, Johnny GUI, Perl/Python runtime | Any modern web browser |
| **Setup Overhead** | Moderate (Binary extraction & path configuration) | Zero (No installation required) |
| **Processing Power** | Local CPU / GPU resources | Remote server processing |
| **Data Privacy** | High (Target file & hash stay local) | Low/Moderate (Requires uploading target file/hash) |
| **Customization** | Full control over wordlists, rules, and masks | Limited to predefined server-side wordlists |
| **Best Used For** | Large scale auditing, custom attacks, strict privacy | Quick testing, lab learning, zero-install environments |

---

## 🛠️ Method 1: Local Cracking (JTR & Johnny GUI)

### Overview
John the Ripper (JTR) is an open-source command-line password recovery engine. Johnny provides a GUI frontend wrapper for `john.exe`, allowing users to configure parameters without CLI commands.

### Detailed Step-by-Step Workflow

#### 1. Setup & Integration
1. Extract the downloaded **John the Ripper** package (e.g., `C:\JohnTheRipper`).
2. Install **Johnny GUI** using its wizard installer.
3. Launch Johnny, open **Settings**, and map the path to `john.exe` (located in `C:\JohnTheRipper\run\john.exe`).

#### 2. Hash Extraction & Formatting
1. Extract the header hash using an offline tool (such as `pdf2john.pl` or `pdf2john.py` located in JTR's `run/` folder) or an online extractor.
2. Open Notepad and format the hash payload:
   * Remove any wrapper syntax such as `b'...'` or surrounding single quotes.
   * Verify the text string begins directly with `$pdf$`.
3. Save the document as `hash1.txt`.

#### 3. Attack Execution
1. Open Johnny, click **Open password file**, and load `hash1.txt`.
2. Click **Start new attack** (uses default hybrid wordlist/rule configurations).
3. Retrieve the cracked credential (`password1`) from the application table once complete.

---

## 🌐 Method 2: Online Cracking (Networkwalks Tools)

### Overview
Networkwalks provides browser-based utilities designed for educational labs. The process separates hash extraction and hash cracking into two distinct, zero-installation web tools.

### Detailed Step-by-Step Workflow

#### 1. Hash Extraction
1. Navigate to the **Networkwalks Hash Calculator** in your browser (`networkwalks.com/hash-calculator/`).
2. Upload `My Locked PDF1.pdf`.
3. The server parses the file metadata and returns the extracted `$pdf$...` hash string.
4. Copy the entire generated output string directly.

#### 2. Password Cracking
1. Open the **Networkwalks Password Cracker** (`networkwalks.com/password-cracker/`).
2. Paste the `$pdf$...` hash string into the input field.
3. Click **Start Attack**. The server cross-references the hash against its internal dictionary.
4. View the plaintext result (`password1`) printed on the web console once matched.

---

## 🔒 Security & Defensive Takeaways

* **Hash Storage Vulnerability**: Encrypted PDF containers do not store plain text passwords; they store hash values derived from key derivation functions (KDFs). Extracting the hash allows offline testing without triggering account lockouts or rate limits.
* **Dictionary Sensitivity**: Weak passwords (e.g., `password1`) are resolved almost instantly regardless of whether local or web-based engines are used.
* **Mitigation**: Use strong passphrases (16+ characters combining uppercase, lowercase, numbers, and special symbols) to render dictionary and brute-force computational attacks mathematically unfeasible.