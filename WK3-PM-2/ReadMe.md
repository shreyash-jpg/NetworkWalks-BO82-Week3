# PDF Password Recovery Walkthrough (Networkwalks Browser-Based Tools)

A complete, step-by-step security testing guide for recovering passwords from encrypted PDF files using web-based tools (**Networkwalks Hash Calculator & Password Cracker**) without requiring local installation.

---

## 📌 Prerequisites

To perform this lab, you only need a modern web browser (Chrome, Firefox, Edge, or Safari) on any operating system (Windows, macOS, Linux, or Kali Linux).

* **Target File**: `My Locked PDF1.pdf`

---

## 📑 Detailed Walkthrough

### Step 1: Obtain the Encrypted File
1. Download `My Locked PDF1.pdf` from your lab portal or the target downloads page.
2. Save the file to a known directory (e.g., `Downloads` or your lab workspace folder).

---

### Step 2: Extract the Hash Signature
1. Open your web browser and go to the [Networkwalks Hash Calculator](https://networkwalks.com/hash-calculator/).
2. Click **Choose File** / **Upload** and select `My Locked PDF1.pdf`.
3. Submit the file. The tool will parse the document structure and extract the stored cryptographic hash string.
4. Highlight and **copy the entire hash string**. 

> **Important**: Ensure you copy the complete string starting with the `$pdf$` prefix without missing any characters or introducing leading/trailing spaces.

---

### Step 3: Crack the Extracted Hash
1. Open a new browser tab and navigate to the [Networkwalks Password Cracker](https://networkwalks.com/password-cracker/).
2. Paste the copied `$pdf$...` hash string into the designated input field.
3. Click **Start Attack** (or **Crack Password**).
4. The tool will run candidate combinations against the hash payload. Wait for the process to complete (execution speed varies based on password complexity).
5. Once complete, the plaintext password (e.g., `password1`) will display on the screen.

---

### Step 4: Verify & Decrypt
1. Locate `My Locked PDF1.pdf` on your machine and open it with your preferred PDF reader.
2. Enter the recovered credential (`password1`) when prompted.
3. Verify that the document unlocks and displays its content successfully.

---

## 🔒 Key Takeaways

* **Hash Extraction**: Password-protected containers do not store plain text; they store cryptographic hashes derived from header metadata. Cracking relies on extracting this header first.
* **Impact of Weak Passwords**: Dictionary attacks can instantly resolve short or common strings like `password1`. 
* **Defense**: Increasing passphrase length (16+ characters) and using non-standard character combinations significantly raises the computational effort required to reverse hashes.
