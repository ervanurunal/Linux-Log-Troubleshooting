## Linux Log Troubleshooting

### Overview

In this lab, I used Linux logs to troubleshoot and identify different system issues. The goal was to use logs to "follow the cookie crumbs" and determine what needed to be fixed.

The lab included five different issues involving:

* Low disk space
* Finding and deleting files
* Updating software
* Finding and terminating processes
* Modifying file permissions

The troubleshooting workflow was:

```text
Review Logs → Identify the Issue → Investigate → Fix → Verify
```

---

### Tools & Resources

* Linux Virtual Machine
* Linux Terminal
* `/var/log`
* `syslog`
* `grep`
* `du`
* `sort`
* `head`
* `sudo`
* `apt-get`
* `ps`
* `kill`
* `chmod`

### Lab Type:
Linux / IT Support Hands-On Lab

---

## 1. Start the Lab

Start the Qwiklabs Linux lab by clicking the **Start Lab** button.

After starting the lab, a Linux shell will be available.

The terminal should display a prompt similar to:

```bash
student@864a6934570a:~$
```

---

## 2. Viewing Logs on Linux

Linux logs are stored in:

```bash
/var/log
```

![1](https://i.imgur.com/lGF7Hap.png)

There are many log files in this directory.

The lab focuses on the **syslog** file.

To view the contents of `syslog`, use:

```bash
cat /var/log/syslog
```

The log can contain a large amount of information.

The five relevant entries contain the phrase:

```text
Qwiklab Error
```

You can use `grep` to filter the logs and find the relevant entries.

![2](https://i.imgur.com/gUEb12i.png)

---

## 3. Troubleshoot Low Disk Space

### Problem

One of the log entries reports:

```text
Aug 23 12:33:21 75b72110ff5a root: Qwiklab Error: Disk space is super low, fix it!
```

The issue is caused by a very large file taking up disk space.

The log does not identify the file, so the first step is to find the largest files.

---

### Find the Largest Files

The `du` command can be used to display disk usage.

The output can be combined with `sort` and `head` to identify the largest files.

```bash
du -a /home | sort -nr | head -n 5
```

#### Command Breakdown

| Command | Purpose                         |
| ------- | ------------------------------- |
| `du`    | Displays disk usage             |
| `-a`    | Includes files and directories  |
| `/home` | Starting directory              |
| `\|`    | Pipes output to another command |
| `sort`  | Sorts the output                |
| `-n`    | Sorts numerically               |
| `-r`    | Sorts in reverse order          |
| `head`  | Displays the first results      |
| `-n 5`  | Displays the top five results   |

The command identifies the largest files under `/home`.

In this lab, the large file was:

```text
/home/lab/storage/ultra_mega_large.txt
```

The file was approximately **5 GB**.

![3](https://i.imgur.com/LSadTxU.png)

---

### Delete the Large File

The file is not needed and is causing the disk-space issue.

Remove it using:

```bash
sudo rm /home/lab/storage/ultra_mega_large.txt
```

After deleting the file, the disk-space issue has been resolved.

![3](https://i.imgur.com/LSadTxU.png)

---

## 4. Find and Delete a Corrupted File

The next issue involves a corrupted file.

The file is located in the `lab` folder in the home directory.

Navigate to the appropriate location and remove:

```text
corrupted_file
```

Use `sudo` with the Linux command for removing files:

```bash
sudo rm corrupted_file
```

![4](https://i.imgur.com/2R4qFdR.png)

---

### Skill Demonstrated

* File navigation
* File identification
* File deletion
* Using `sudo`
* Troubleshooting files

---

## 5. Update VLC on Linux

The next issue involves the VLC media player package.

Use `apt-get` with `sudo` to identify and install missing dependencies:

```bash
sudo apt-get -f install
```

The `-f` flag can be used to force the installation or update of a package when there are potential conflicts or errors.

Then, check the status of the VLC package:

![5](https://i.imgur.com/S3wbiie.png)

---

### Skill Demonstrated

* Linux package management
* Software troubleshooting
* Dependency management
* `apt-get`
* Using `sudo`

---

## 6. Find and Terminate a Process

The next issue involves a process named:

```text
totally_not_malicious
```

First, use `ps -aux` and `grep` to find the process:

```bash
ps -aux | grep totally_not_malicious
```

Identify the **Process ID (PID)**.

Then terminate the process using:

```bash
sudo kill [PROCESS_ID]
```

---

### Verify the Process

Run the search again:

```bash
ps -aux | grep totally_not_malicious
```

This confirms whether the process has been terminated.

![6](https://i.imgur.com/aZmdoeU.png)

---

### Skill Demonstrated

* Process monitoring
* PID identification
* `ps`
* `grep`
* `kill`
* `sudo`

---

## 7. Modify File Permissions

The final issue involves the file:

```text
super_secret_file.txt
```

The lab requires changing the permissions so that the file has:

* Read
* Write
* Execute

permissions.

![7](https://i.imgur.com/4wXF6y3.png)

---

## Troubleshooting Workflow

The overall process used in this lab was:

```text
1. Review Linux Logs
        ↓
2. Find "Qwiklab Error"
        ↓
3. Identify the Problem
        ↓
4. Investigate the Cause
        ↓
5. Apply the Appropriate Command
        ↓
6. Verify the Fix
```

---

## Key Linux Commands

| Command   | Purpose                                |
| --------- | -------------------------------------- |
| `cat`     | Displays the contents of a file        |
| `grep`    | Searches for matching text             |
| `du`      | Displays disk usage                    |
| `sort`    | Sorts command output                   |
| `head`    | Displays the beginning of output       |
| `rm`      | Removes files                          |
| `cd`      | Changes directories                    |
| `apt-get` | Manages software packages              |
| `ps`      | Displays running processes             |
| `kill`    | Terminates a process                   |
| `chmod`   | Changes file permissions               |
| `sudo`    | Executes commands with root privileges |

---

## Cybersecurity Relevance

Log analysis is an important skill for an **IT Support Specialist** and **SOC Analyst**.

In this lab, I practiced a basic security and troubleshooting workflow:

```text
Log Collection
      ↓
Log Filtering
      ↓
Identify Abnormal Activity
      ↓
Investigate
      ↓
Take Action
      ↓
Verify
```

These skills can be applied when investigating:

* Suspicious processes
* System errors
* Disk-space problems
* Unauthorized file changes
* Software issues
* Permission problems

Understanding Linux logs is especially useful when working with Linux servers and security monitoring tools.

---

## Troubleshooting Notes

### Too many log entries

Use `grep` to filter the logs:

```bash
grep "Qwiklab Error" /var/log/syslog
```

### Finding large files

Use:

```bash
du -a /home | sort -nr | head -n 5
```

### Process still running

Search for the process again:

```bash
ps -aux | grep totally_not_malicious
```

Make sure you are using the correct PID with:

```bash
sudo kill [PROCESS_ID]
```

### Permission changes fail

Use `sudo` to execute the permission command with root privileges:

```bash
sudo chmod 777 super_secret_file.txt
```

---

## Skills Demonstrated

* Linux log analysis
* Linux troubleshooting
* Command-line navigation
* File management
* Disk-space troubleshooting
* Package management
* Process management
* Process termination
* File permissions
* `sudo`
* `grep`
* `du`
* `sort`
* `head`
* `ps`
* `kill`
* `chmod`
* `apt-get`

---

### Final Takeaway

This lab demonstrated how Linux logs can be used to **identify, investigate, and resolve system issues**.

The most important workflow I practiced was:

```text
Read the Log
     ↓
Find the Problem
     ↓
Investigate
     ↓
Apply the Fix
     ↓
Verify
```

This hands-on experience strengthened my Linux troubleshooting, command-line, log analysis, and system administration skills, which are also relevant to **SOC Analyst** work.
