# Ciphathon CTF 2026 — Writeups

**Team:** Dystopian Debuggers

**Members:**
- Sarthak Warale ([@glitchseeker](https://github.com/glitchseeker))
- Sameep Navale ([@abcd](https://github.com/abcd))
- Shivam Khopade ([@SshivamK](https://github.com/SshivamK))
- Suyog Jadhav

---
    
## Challenges Solved

### 🌐 Web
- [Key Heist Level 1](Web/Key%20Heist%20Level%201/Key%20Heist%20Level%201.md)
- [Shaastra Merch Store](Web/Shaastra%20Merch%20Store/Shaastra%20Merch%20Store.md)
- [Nothing to See](Web/Nothing%20to%20See/Nothing%20to%20See.md)

### 🔍 Forensics
- [Forensic Node #337](Forensics/Forensic%20Node%20%23337/Forensic%20Node%20%23337.md)
- [Archive Node #99X](Forensics/Archive%20Node%20%2399X/Archive%20Node%20%2399X.md)
- [Hidden in the Noise](Forensics/Hidden%20in%20the%20Noise/Hidden%20in%20the%20Noise.md)
- [DNS Node](Forensics/DNS%20Node/DNS%20Node.md)
- [Image Node](Forensics/Image%20Node/Image%20Node.md)
- [Artifact Node #55A](Forensics/Artifact%20Node%20%2355A/Artifact%20Node%20%2355A.md)
- [Disk Node](Forensics/Disk%20Node/Disk%20Node.md)
- [Memory Node](Forensics/Memory%20Node/Memory%20Node.md)

### ⚙️ Reverse Engineering
- [XOR Shard](Reverse%20engineering/XOR%20Shard/XOR%20Shard.md)
- [Flux Node](Reverse%20engineering/Flux%20Node/Flux%20Node.md)
- [Core #900](Reverse%20engineering/Core%20%23900/Core%20%23900.md)
- [Bitstream Node](Reverse%20engineering/Bitstream%20Node/Bitstream%20Node.md)
- [Mask Node](Reverse%20engineering/Mask%20Node/Mask%20Node.md)
- [Strings](Reverse%20engineering/Strings/Strings.md)
- [Transform Node](Reverse%20engineering/Transform%20Node/Transform%20Node.md)
- [Temporal Node #777](Reverse%20engineering/Temporal%20Node%20%23777/Temporal%20Node%20%23777.md)
- [Fragment Node #100](Reverse%20engineering/Fragment%20Node%20%23100/Fragment%20Node%20%23100.md)

### 🕵️ OSINT
- [The Redacted Ledger](Osint/The%20Redacted%20Ledger/The%20Redacted%20Ledger.md)
- [Beside the Monument](Osint/Beside%20the%20Monument/Beside%20the%20Monument.md)
- [Digital Footprints](Osint/Digital%20Footprints/Digital%20Footprints.md)
- [The Quiet Journey](Osint/The%20Quiet%20Journey/The%20Quiet%20Journey.md)

### 🔐 Cryptography
- [Something Sketchy](Cryptography/Something%20Sketchy/Something%20Sketchy.md)

---

## 🛠️ Tools Used

Throughout the CTF, we utilized a variety of tools across different categories:

**Web Security:**
* **Cookie Editor:** Used for manipulating JWT tokens and exploiting integer overflows in cart endpoints.

**Forensics:**
* **`strings`:** Used recursively to extract hidden plaintext flags from corrupted containers, corrupted images, and disk fragments.
* **Aperisolve / `zsteg`:** Used heavily for LSB steganography analysis and extracting hidden data from image channels.
* **Archive Utilities (`unzip`):** Used for recursive extraction of nested ZIP chains.
* **Memory Forensics Tools:** Used to extract strings and volatile context from `.raw` memory dumps.

**Reverse Engineering:**
* **`file`:** Essential for initial binary analysis to identify PE32+ MS Windows executables.
* **PyInstxtractor:** Used meticulously to unpack compiled PyInstaller Windows executables.
* **Pylingual.io:** An online tool used to decompile the extracted `.pyc` Python bytecodes back into readable source code.
* **Python Scripts:** Custom scripting used extensively to reverse various encryption mechanisms (XOR, Base64, Bit-rotation, Linear Congruential Generators).

**OSINT:**
* **Google Advanced Search / Dorking:** Leveraged to filter specific news articles and track cross-platform usernames.
* **Reverse Image Search:** Used for geospatial intelligence to identify monuments and rivers.
* **Social Media OSINT:** Tracked digital footprints seamlessly across Instagram and GitHub repositories.

---

## 🧠 What We Learned

Participating in Ciphathon CTF 2026 provided several key takeaways and areas of improvement:

1. **Python Executable Reversing is Crucial:** A large portion of the RE challenges relied heavily on PyInstaller binaries. We solidified our workflow of `binary -> pyinstxtractor -> pylingual.io -> python script` to quickly overcome these challenges.
2. **Never Ignore the "Obvious" in Web:** From hidden HTML source code comments to easily manipulatable JWTs using standard developer tools, the basics often yielded the most direct path to the flag.
3. **OSINT Requires Persistence:** Gathering digital footprints requires pivoting. Finding a user on Instagram was only step one; knowing to check their bio for secondary usernames to pivot to GitHub was the actual breakthrough.
4. **Steganography Automation:** Relying on automated tools like Aperisolve saved a lot of time compared to manually performing LSB extraction using raw scripting.
5. **Always check `strings`:** Simple static analysis with the `strings` utility proved invaluable, not just in Forensics, but in RE and disk image challenges. Many flags require no complex reversing, just thorough observation.