# Bandit Levels 5-20 Solutions

## Level 5 → Level 6

### 🎯 Goal
Find a file in the `inhere` directory with these properties:
- Human-readable
- 1033 bytes in size
- Not executable

### 🚀 Solution
```bash
cd inhere
find . -type f -size 1033c
cat ./maybehere07/.file2
```

### 🔐 Password
```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

### 💡 What I Learned
- Using `find` with size filters (`-size 1033c` where `c` = bytes)
- Combining multiple criteria in file searches
- Hidden files can be found with `find` even without `-name` flags

### 🔧 Commands Used
- `find . -type f -size 1033c` - Find files of exact size

---

## Level 6 → Level 7

### 🎯 Goal
Find a file anywhere on the server with:
- Owned by user `bandit7`
- Owned by group `bandit6`
- 33 bytes in size

### 🚀 Solution
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

### 🔐 Password
```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

### 💡 What I Learned
- Searching system-wide from root (`/`)
- Filtering by user and group ownership
- Suppressing permission errors with `2>/dev/null`
- Understanding file ownership in Linux

### 🔧 Commands Used
- `find / -user X -group Y -size Zc` - System-wide search with filters
- `2>/dev/null` - Redirect errors to null (suppress them)

---

## Level 7 → Level 8

### 🎯 Goal
Find the password in `data.txt` next to the word "millionth"

### 🚀 Solution
```bash
grep "millionth" data.txt
```

### 🔐 Password
```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

### 💡 What I Learned
- Using `grep` to search for text patterns in files
- Pattern matching to find specific keywords

### 🔧 Commands Used
- `grep "pattern" file` - Search for text in file

---

## Level 8 → Level 9

### 🎯 Goal
Find the only line in `data.txt` that appears exactly once (unique among duplicates)

### 🚀 Solution
```bash
sort data.txt | uniq -u
```

### 🔐 Password
```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

### 💡 What I Learned
- `sort` is required before `uniq` for it to work correctly
- `uniq -u` shows only unique lines (appearing once)
- Piping commands together to create processing pipelines

### 🔧 Commands Used
- `sort` - Sort lines alphabetically
- `uniq -u` - Show only unique lines
- `|` - Pipe operator to chain commands

---

## Level 9 → Level 10

### 🎯 Goal
Find human-readable string in binary file `data.txt` preceded by several '=' characters

### 🚀 Solution
```bash
strings data.txt | grep "=="
```

### 🔐 Password
```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

### 💡 What I Learned
- Binary files can't be searched with regular grep
- `strings` extracts human-readable text from binary files
- Combining `strings` with `grep` to filter output

### 🔧 Commands Used
- `strings` - Extract printable strings from binary files
- `grep` - Filter for specific patterns

---

## Level 10 → Level 11

### 🎯 Goal
Decode base64 encoded data in `data.txt`

### 🚀 Solution
```bash
base64 -d data.txt
```

### 🔐 Password
```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

### 💡 What I Learned
- Base64 encoding represents binary data as ASCII text
- `-d` flag decodes base64 data
- Common encoding method for data transmission

### 🔧 Commands Used
- `base64 -d` - Decode base64 data

---

## Level 11 → Level 12

### 🎯 Goal
Decode ROT13 encoded text in `data.txt`

### 🚀 Solution
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### 🔐 Password
```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

### 💡 What I Learned
- ROT13 is a simple substitution cipher (shift by 13)
- `tr` translates characters from one set to another
- Understanding character mapping and rotation

### 🔧 Commands Used
- `tr 'A-Za-z' 'N-ZA-Mn-za-m'` - ROT13 decoding

---

## Level 12 → Level 13

### 🎯 Goal
Decompress repeatedly compressed file (hexdump reversed)

### 🚀 Solution
```bash
cd /tmp
mydir=$(mktemp -d)
cd "$mydir"
cp /home/bandit12/data.txt .
xxd -r data.txt > data
file data  # Check type repeatedly
# Decompress based on type:
# gzip: mv data data.gz && gunzip data.gz
# bzip2: mv data data.bz2 && bunzip2 data.bz2
# tar: tar xf data
# Repeat until text file found
cat data8
```

### 🔐 Password
```
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

### 💡 What I Learned
- Reversing hexdumps with `xxd -r`
- Identifying file types with `file` command
- Handling multiple compression layers (gzip, bzip2, tar)
- Working in `/tmp` for write permissions

### 🔧 Commands Used
- `xxd -r` - Reverse hexdump
- `file` - Identify file type
- `gunzip`, `bunzip2`, `tar xf` - Decompression tools

---

## Level 13 → Level 14

### 🎯 Goal
Use SSH private key to login as bandit14 and read password file

### 🚀 Solution
```bash
ssh -i sshkey.private bandit14@localhost -p 2220
cat /etc/bandit_pass/bandit14
```

### 🔐 Password
```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

### 💡 What I Learned
- SSH key-based authentication with `-i` flag
- Connecting to localhost to change user context
- Restricted file access requires proper user permissions

### 🔧 Commands Used
- `ssh -i keyfile user@host` - SSH with private key authentication

---

## Level 14 → Level 15

### 🎯 Goal
Submit current password to port 30000 on localhost using netcat

### 🚀 Solution
```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

### 🔐 Password
```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

### 💡 What I Learned
- Using `nc` (netcat) for network communication
- Piping data to network services
- Port-based service interaction

### 🔧 Commands Used
- `nc` - Netcat for network connections
- `|` - Pipe data between commands

---

## Level 15 → Level 16

### 🎯 Goal
Submit password to port 30001 using SSL/TLS encryption

### 🚀 Solution
```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

### 🔐 Password
```
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

### 💡 What I Learned
- Using OpenSSL for encrypted connections
- SSL/TLS client operations
- Secure service communication

### 🔧 Commands Used
- `openssl s_client -connect` - SSL/TLS client connection
- `-quiet` - Reduce verbose output

---

## Level 16 → Level 17

### 🎯 Goal
Scan ports 31000-32000, find SSL service that returns RSA private key

### 🚀 Solution
```bash
nmap 127.0.0.1 -p 31000-32000
ncat 127.0.0.1 --ssl 31790
# Save private key
cd /tmp
nano pvt.key  # Paste RSA key
chmod 400 pvt.key
ssh -i pvt.key bandit17@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit17
```

### 🔐 Password
```
EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```

### 💡 What I Learned
- Port scanning with `nmap`
- Testing SSL connections with `ncat --ssl`
- Proper file permissions for private keys (400)
- Saving and using RSA private keys

### 🔧 Commands Used
- `nmap` - Network port scanner
- `ncat --ssl` - SSL connection testing
- `chmod 400` - Set restrictive permissions

---

## Level 17 → Level 18

### 🎯 Goal
Find the changed line between two files

### 🚀 Solution
```bash
diff passwords.old passwords.new
```

### 🔐 Password
```
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

### 💡 What I Learned
- `diff` compares files line by line
- `<` indicates lines from first file
- `>` indicates lines from second file

### 🔧 Commands Used
- `diff file1 file2` - Compare two files

---

## Level 18 → Level 19

### 🎯 Goal
Read `readme` file but `.bashrc` logs you out immediately

### 🚀 Solution
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```

### 🔐 Password
```
cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```

### 💡 What I Learned
- Executing commands via SSH without interactive shell
- Bypassing login scripts
- Non-interactive SSH usage

### 🔧 Commands Used
- `ssh user@host "command"` - Execute remote command directly

---

## Level 19 → Level 20

### 🎯 Goal
Use setuid binary to execute commands as bandit20

### 🚀 Solution
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

### 🔐 Password
```
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```

### 💡 What I Learned
- Setuid binaries run with file owner's permissions
- Privilege escalation through setuid
- Accessing restricted files via privilege elevation

### 🔧 Commands Used
- `./setuid-binary command` - Execute with elevated privileges

---

## 📚 Advanced Commands Summary

| Command | Purpose | Example |
|---------|---------|---------|
| `find / -user X -group Y` | Search by ownership | `find / -user bandit7` |
| `sort file \| uniq -u` | Find unique lines | Filter duplicates |
| `strings binary` | Extract readable text | From binary files |
| `base64 -d` | Decode base64 | `base64 -d file` |
| `tr 'A-Z' 'N-ZA-M'` | Character translation | ROT13 decoding |
| `xxd -r` | Reverse hexdump | Convert hex to binary |
| `nmap host -p range` | Port scanning | `nmap localhost -p 31000-32000` |
| `openssl s_client` | SSL/TLS client | Encrypted connections |
| `diff file1 file2` | Compare files | Find differences |
| `ssh user@host "cmd"` | Remote command | Non-interactive execution |

---

**Completed:** Levels 0-20 ✅
