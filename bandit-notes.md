# OverTheWire Bandit — Solutions and Notes

Completed levels from the Bandit wargame at overthewire.org.
Bandit teaches Linux command-line skills through hands-on security challenges.

---

## Level 0 — First SSH Login

**Goal:** Log into the Bandit server using SSH.

**Command used:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

**What I learned:**
- SSH (Secure Shell) is used to remotely log into another computer securely
- Format: `ssh username@host -p port`
- The `-p` flag specifies a non-default port (default SSH port is 22)
- When typing a password in Linux, nothing appears on screen — that is normal behaviour

**Password found:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

---

## Level 0 → 1 — Read a File

**Goal:** Find the password stored in a file called `readme` in the home directory.

**Commands used:**
```bash
ls
cat readme
```

**What I learned:**
- `ls` lists all files in the current directory
- `cat` reads and prints the contents of a file to the terminal
- The home directory `~` is where you land after logging in

**Password found:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

---

## Level 1 → 2 — File Named with a Dash

**Goal:** Read a file called `-` (a single dash).

**Problem:** `cat -` does not work because the terminal interprets `-` as "read from keyboard input" not as a filename.

**Command used:**
```bash
cat ./-
```

**What I learned:**
- `./` means "in the current directory" — it forces the terminal to treat `-` as a filename
- Special characters like `-` need to be handled carefully in Linux
- This trick is commonly used in CTF challenges

**Password found:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

---

## Level 2 → 3 — Filename with Spaces

**Goal:** Read a file called `spaces in this filename`.

**Problem:** `cat spaces in this filename` fails because the terminal treats each word as a separate argument.

**Command used:**
```bash
cat ./'abc'
```

**Alternative solutions:**
```bash
cat "spaces in this filename"
cat spaces\ in\ this\ filename
```

**What I learned:**
- Filenames with spaces must be wrapped in quotes or each space escaped with `\`
- Tab key autocompletes filenames including spaces — very useful
- Single quotes `'` and double quotes `"` both work for wrapping filenames

**Password found:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

---

## Level 3 → 4 — Hidden File

**Goal:** Find a hidden file inside the `inhere` directory.

**Problem:** Normal `ls` does not show hidden files. Hidden files in Linux start with a `.` (dot).

**Commands used:**
```bash
ls -a
cat ...
```

**What I learned:**
- `ls -a` shows ALL files including hidden ones (files starting with `.`)
- `ls -la` shows hidden files with full details including permissions and size
- Hidden files are commonly used by malware and attackers to hide data
- The `-a` flag stands for "all"

**Password found:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

---

## Level 4 → 5 — Find Human-Readable File

**Goal:** Find the only human-readable file out of 10 files in the `inhere` directory.

**Commands used:**
```bash
find . -type f -size 1333c
```

**What I learned:**
- `find` is one of the most powerful Linux commands for locating files
- `-type f` means search for files only (not directories)
- `-size 1333c` means exactly 1333 bytes (`c` = bytes)
- The `file` command can also identify file types: `file ./-file0*`
- "Human-readable" means ASCII text — not binary data

**Password found:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

---

## Level 5 → 6 — Find File by Owner and Group

**Goal:** Find a file owned by user `bandit7`, group `bandit6`, and exactly 33 bytes in size — anywhere on the server.

**Command used:**
```bash
find / -user bandit7 -group bandit6 -size 33b 2>/dev/null
```

**What I learned:**
- `find /` searches the entire filesystem starting from root
- `-user bandit7` filters by file owner
- `-group bandit6` filters by group ownership
- `-size 33b` means exactly 33 bytes
- `2>/dev/null` redirects error messages to nowhere so they don't clutter the output — very useful when searching the whole filesystem
- File ownership is a critical concept in Linux security and privilege escalation

**Password found:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

---

## Level 6 → 7 — Search Inside a File with grep

**Goal:** Find the password next to the word "millionth" in a large file called `data.txt`.

**Command used:**
```bash
grep "" data.txt
```

**Better command for this level:**
```bash
grep "millionth" data.txt
```

**What I learned:**
- `grep` searches for a pattern inside a file and prints matching lines
- Format: `grep "search term" filename`
- `grep` is used constantly in security — searching logs, config files, finding credentials
- Can search recursively through directories with `grep -r "term" /path`

**Password found:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

---

## Level 7 → 8 — Find the Unique Line

**Goal:** Find the one line in `data.txt` that appears only once.

**Command used:**
```bash
sort data.txt | uniq -u
```

**What I learned:**
- `sort` arranges lines alphabetically — required before using `uniq`
- `uniq` removes or identifies duplicate lines
- `uniq -u` prints only lines that appear exactly once
- The `|` pipe symbol sends the output of one command into the next
- Piping commands together is a core Linux skill used in log analysis and forensics

**Password found:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

---

## Level 8 → 9 — Find Human-Readable Strings in Binary File

**Goal:** Find the password hidden inside a binary file — it is near several `=` signs.

**Command used:**
```bash
strings data.txt | grep "="
```

**What I learned:**
- `strings` extracts all human-readable text from any file, including binary files
- Piping into `grep "="` filters to lines containing `=` signs
- This technique is used in malware analysis — running `strings` on a suspicious file reveals readable content like URLs, usernames, and commands hidden inside
- Essential tool for digital forensics

**Password found:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

---

## Level 9 → 10 — Decode Base64

**Goal:** The password is stored in `data.txt` encoded in Base64. Decode it.

**Command used:**
```bash
base64 -d data.txt
```

**What I learned:**
- Base64 is an encoding scheme that converts binary data into text characters
- It is NOT encryption — anyone can decode it instantly
- Base64 encoded text usually ends with `=` or `==` padding
- Commonly seen in CTFs, email attachments, web tokens (JWT), and malware obfuscation
- `-d` flag means decode

**Password found:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

---

## Commands Summary

| Command | What it does |
|---------|-------------|
| `ssh user@host -p port` | Connect to a remote server securely |
| `ls` | List files in current directory |
| `ls -a` | List all files including hidden ones |
| `ls -la` | List all files with full details and permissions |
| `cat filename` | Read and print a file |
| `cat ./-` | Read a file named with a dash |
| `find / -user X -group Y -size Zb` | Find files by owner, group and size |
| `find . -type f -size Xc` | Find files by size in bytes |
| `grep "term" file` | Search for text inside a file |
| `sort file | uniq -u` | Find lines that appear only once |
| `strings file` | Extract readable text from binary files |
| `base64 -d file` | Decode a base64-encoded file |
| `2>/dev/null` | Hide error messages from output |

---

## Key Concepts Learned

- **SSH** — how to connect to remote servers, the foundation of server administration and pentesting
- **Hidden files** — files starting with `.` are hidden by default in Linux
- **File ownership** — every file has a user owner and a group owner, critical for Linux privilege escalation
- **Pipes `|`** — chain commands together, output of one becomes input of the next
- **Base64** — common encoding used in CTFs, web tokens, and malware — not encryption
- **`strings`** — essential forensics tool for analysing suspicious files
- **`2>/dev/null`** — redirect errors away to get clean output when searching the whole filesystem
