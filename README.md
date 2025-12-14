<img width="1536" height="1024" alt="banner" src="https://github.com/user-attachments/assets/8ed1c8a1-9880-4828-9732-85302f06397e" />

# gtfobinSUID V1.2

**Developed by [strikoder](https://www.youtube.com/@strikoder)**  

`gtfobinSUID`  is a lightweight Python tool for automating SUID/SGID binary enumeration. It compares discovered binaries against the [GTFOBins](https://gtfobins.github.io) database and supports both online and offline modes.
In offline mode, it uses a local database file (db.txt), which can be automatically updated by scraping the latest entries from GTFOBins.

## 🎥 Demo

![gtfobinSUID demo](https://github.com/user-attachments/assets/f96be760-cfad-4845-9f06-82bb0bafbcb1)

---

## 🔹 Features

- Works on Linux, macOS, and Windows
- Handles versioned binary names (python3, perl5.42, etc.)
- Prints the command to enumerate SUID/GUID on Linux systems on demand
- Minimal, no dependencies beyond `requests` *(likely preinstalled on Kali Linux)*
- Shows hints for binaries that might have vulnearbilites when they have SUID enabled like pkexec and sudo 
- Checks if a binary exists on GTFOBins under **SUID** or **Limited SUID** and prints `[FOUND]`, `[FOUND - Limited SUID]`, or `[NOT FOUND]` as it processes

---

## Flags

- **--online (Default)**: fetches live data directly from GTFOBins
- **--update-db**: automatically pulls all GTFOBins SUID and Limited SUID entries
- **--offline (Auto-Switch with no network)**: uses a local `db.txt` for environments without internet

---

## Installation

Choose your preferred installation method:

### Method 1: pipx
Install in an isolated environment using pipx:
```bash
pipx install gtfobinsuid
```

### Method 2: pip
Install globally or in a virtual environment:
```bash
pip3 install gtfobinsuid
```

### Method 3: From Source
Clone the repository and install dependencies:
```bash
git clone https://github.com/strikoder/gtfobinSUID.git
cd gtfobinsuid
pip install requests
```

### Method 4: Standalone Script
Download and run directly without installation:

**Using wget:**
```bash
wget -q -O gtfobinsuid.py "https://raw.githubusercontent.com/strikoder/gtfobinSUID/main/gtfobinsuid.py"
chmod +x gtfobinsuid.py
./gtfobinsuid.py
```

**Using curl:**
```bash
curl -sL -o gtfobinsuid.py "https://raw.githubusercontent.com/strikoder/gtfobinSUID/main/gtfobinsuid.py"
chmod +x gtfobinsuid.py
./gtfobinsuid.py
```

---

## Usage

### 1. Basic usage
Paste your SUID/SGID enum output directly:
```bash
python3 gtfobinsuid.py
```

Then paste something like:
```
/usr/bin/find
/usr/bin/passwd
/usr/bin/sudo
/bin/mount
```

Press **Ctrl+d** (Linux/macOS) or **Ctrl+z + Enter** (Windows) to finish.  
You’ll see immediate output:
```
[FOUND] find -> https://gtfobins.github.io/gtfobins/find/
[NOT FOUND] sudo
    [!] HINT: 'sudo' with SUID might indicate CVE exploits or misconfigurations (check Baron Samedit & version vulnerabilities)
[NOT FOUND] mount
```
### 2. Force online or offline
- Force online only:
  ```bash
  python3 gtfobinsuid.py --online
  ```
- Force offline mode (requires `db.txt`):
  ```bash
  python3 gtfobinsuid.py --offline
  ```
### 3. Update the local database
You can refresh `db.txt` automatically from GTFOBins:

```bash
python3 gtfobinsuid.py --update-db
```

This will:
- Fetch all SUID and Limited SUID binaries directly from the GTFOBins website
- Save them to `db.txt`
- Print how many entries were found

Example output:
```
[*] Fetching GTFOBins lists...
[+] Database updated successfully: db.txt
    195 SUID entries
    64 Limited SUID entries
```

---

##  How it works

1. Extracts basenames from your pasted enumeration results.  
   Example: `/usr/bin/sudo` → `sudo`
2. Checks each binary:
   - If online: queries the GTFOBins page for that binary.
   - If offline: looks up the name in `db.txt`.
3. Prints result immediately for each binary.

---

## 🧑‍💻 Author

**Strikoder**  
Penetration Tester & ex AI Engineer

