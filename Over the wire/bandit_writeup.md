# Bandit Wargame Writeup (Levels 0 → 13)

This writeup covers my solutions for the Bandit wargame hosted at [OverTheWire](https://overthewire.org/wargames/bandit/).  
Each level introduces Linux command-line techniques useful for security and CTF challenges.

---

## Bandit1 → Bandit2
**Challenge:** Read the contents of a simple file.  
```bash
cat readme
```
**Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

---

## Bandit2 → Bandit3
**Challenge:** File named `-` (interpreted as stdin/stdout).  
```bash
cat ./-
```
**Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

---

## Bandit3 → Bandit4
**Challenge:** File name contains spaces.  
```bash
cat ./"spaces in this filename"
```
**Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

---

## Bandit4 → Bandit5
**Challenge:** Hidden file inside the directory.  
```bash
ls -a
cat .hidden
```
**Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

---

## Bandit5 → Bandit6
**Challenge:** File among many, needed manual search.  
```bash
cat inhere/*
```
**Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

## Bandit6 → Bandit7
**Challenge:** Find file with specific properties.  
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /path/to/file
```
**Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

## Bandit7 → Bandit8
**Challenge:** Search file for a specific keyword.  
```bash
grep "millionth" data.txt
```
**Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

## Bandit8 → Bandit9
**Challenge:** Find unique line in file.  
```bash
sort data.txt | uniq -u
```
**Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

## Bandit9 → Bandit10
**Challenge:** Binary file, need to extract readable strings.  
```bash
strings data.txt | grep "==="
```
**Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

---

## Bandit10 → Bandit11
**Challenge:** Base64 encoded text.  
```bash
base64 -d data.txt
```
**Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

## Bandit11 → Bandit12
**Challenge:** ROT13 encoded text.  
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
**Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

---

## Bandit12 → Bandit13
**Challenge:** Multiple layers of compression.  
```bash
xxd -r data.txt > data.gz
gunzip data.gz
bunzip2 data.bz2
tar -xvf data.tar
# repeat until last file is extracted
```
**Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`

---

## Bandit13 → Bandit14
**Challenge:** Login with SSH key provided in home directory.  
```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
**Password:** *(Not needed, direct login with key)*
