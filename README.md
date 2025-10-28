# gtfobinSUID

**Developed by [strikoder](https://www.youtube.com/@strikoder)**  


`gtfobinSUID` is a lightweight Python tool that automates the process of checking binaries discovered during SUID/SGID enumeration against the [GTFOBins](https://gtfobins.github.io) database.  
It works in both **online** and **offline** modes and can also **update its own local database** (`db.txt`) by scraping GTFOBins automatically.

## 🎥 Demo

![gtfobinSUID demo](https://raw.githubusercontent.com/strikoder/gtfobinSUID/main/demo.gif)

---

## 🔹 Features
- Checks if a binary exists on GTFOBins under **SUID** or **Limited SUID**
- **Online mode**: fetches live data directly from GTFOBins
- **Offline mode**: uses a local `db.txt` for environments without internet
- **Auto-detect** mode: automatically switches to offline when no network
- **Database updater**: `--update-db` automatically pulls all GTFOBins SUID and Limited SUID entries
- **Real-time output**: prints `[FOUND]`, `[FOUND - Limited SUID]`, or `[NOT FOUND]` as it processes
- Minimal, no dependencies beyond `requests`
- Works on Linux, macOS, and Windows
---

## Installation

```bash
git clone https://github.com/strikoder/gtfobinSUID.git
cd gtfobinsuid
pip install requests
```
Or if you hate cloning like me, you can install only the main python file:
```bash
wget -q -O gtfobinsuid.py "https://raw.githubusercontent.com/strikoder/gtfobinSUID/main/gtfobinsuid.py" && chmod +x gtfobinsuid.py
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
[FOUND] sudo -> https://gtfobins.github.io/gtfobins/sudo/
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

