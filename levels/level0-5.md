# Bandit Levels 0-5 Solutions

## Level 0: Initial Connection

### 🎯 Goal
Learn how to connect to the Bandit server using SSH.

### 🚀 Solution
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
# Password: bandit0
```

### 💡 What I Learned
- How to use SSH command for remote login
- Specifying non-default SSH port with `-p`

---

## Level 0 → Level 1

### 🎯 Goal
Find password in a file called `readme` in home directory.

### 🚀 Solution
```bash
ls
cat readme
```

### 🔐 Password
```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

### 💡 What I Learned
- Using `ls` to list directory contents
- Using `cat` to display file contents

---

## Level 1 → Level 2

### 🎯 Goal
Password stored in a file called `-` in home directory.

### 🚀 Challenge
The filename `-` is interpreted as stdin by most commands.

### 🚀 Solution
```bash
cat ./-
```

### 🔐 Password
```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

### 💡 What I Learned
- Special filenames need careful handling
- Using `./` prefix treats dash as part of path

---

## Level 2 → Level 3

### 🎯 Goal
Password in file called `spaces in this filename`.

### 🚀 Solution
```bash
cat "spaces in this filename"
```

### 🔐 Password
```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

### 💡 What I Learned
- Filenames with spaces need quotes or escaping
- Tab completion auto-escapes spaces

---

## Level 3 → Level 4

### 🎯 Goal
Password in hidden file in `inhere` directory.

### 🚀 Solution
```bash
cd inhere
ls -a
cat ./...Hiding-From-You
```

### 🔐 Password
```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

### 💡 What I Learned
- Hidden files start with `.` (dot)
- `ls -a` reveals hidden files

---

## Level 4 → Level 5

### 🎯 Goal
Password in only human-readable file in `inhere` directory.

### 🚀 Solution
```bash
cd inhere
file ./*
cat ./-file07
```

### 🔐 Password
```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

### 💡 What I Learned
- `file` command identifies file types
- Always check file type before using `cat` on unknown files
- Binary files can corrupt terminal output

---

## 📚 Commands Summary

| Command | Purpose |
|---------|---------|
| `ssh -p PORT user@host` | Connect to remote server |
| `ls` | List directory contents |
| `ls -a` | List all files (including hidden) |
| `cat filename` | Display file contents |
| `cat ./filename` | Read file with relative path |
| `cat "file name"` | Read file with spaces |
| `file path` | Identify file type |
| `cd directory` | Change directory |

---

**Next:** Levels 5-10 (coming soon)
