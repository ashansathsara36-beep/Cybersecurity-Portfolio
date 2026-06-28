# Linux File Permissions: Securing Research Data

## 📖 Scenario
I am a security analyst at a research hospital. The lead researcher, `researcher2`, stores sensitive patient trial data in the `/home/researcher2/projects/` directory. My task was to review the current permissions and restrict unauthorized access to ensure only the `researcher2` user and the `research_team` group have access.

## 🎯 Objective
To enforce the **Principle of Least Privilege** by removing world-readable and write permissions from sensitive files, ensuring only authorized personnel can view or modify them.

## 🛠️ Tools Used
- Linux Bash Shell
- Commands: `ls -la`, `chmod`, `sudo`

---

## 🔍 Step 1: Check Current Permissions
I used `ls -la` to list all files, including hidden ones, and display the permission strings for each.

### Command Entered:
```bash
ls -la /home/researcher2/projects/
```

### Output Received (Simulated):
```bash
drwxr-xr-x 2 researcher2 research_team 4096 Jun 20 10:00 .
drwxr-xr-x 4 researcher2 research_team 4096 Jun 20 09:45 ..
-rw-r--r-- 1 researcher2 research_team  1024 Jun 20 09:50 patient_data.txt
-rw-r--r-- 1 researcher2 research_team   512 Jun 20 09:55 trial_results.csv
```

> **Analysis:** The file `patient_data.txt` has `-rw-r--r--`. The last `r--` means **"Others"** (any user on the system) can **read** it. This is a critical vulnerability.

---

## 🔧 Step 2: Modify the Permissions
I used the `chmod` command to remove read and write permissions for the "Others" group.

### Command Entered:
```bash
sudo chmod 740 /home/researcher2/projects/patient_data.txt
```

### Breakdown of `740`:
- **7** (Owner = researcher2): Read (4) + Write (2) + Execute (1) = **Full Access**.
- **4** (Group = research_team): Read (4) only.
- **0** (Others): **No access** (Read, Write, Execute all removed).

---

## ✅ Step 3: Verify the Fix
I ran `ls -la` again to confirm the permissions were updated successfully.

### Command Entered:
```bash
ls -la /home/researcher2/projects/patient_data.txt
```

### Verified Output:
```bash
-rwxr----- 1 researcher2 research_team 1024 Jun 20 09:50 patient_data.txt
```

> **Result:** The file now shows `-rwxr-----`. The trailing `---` confirms that **"Others" have zero permissions**. The data is now secure and compliant with internal privacy policies.

## 📚 Summary of Commands Used
| Command | Purpose |
| :--- | :--- |
| `ls -la` | Lists all files with detailed permission strings. |
| `sudo chmod 740 [file]` | Changes file permissions to 740 using superuser privileges. |
| `sudo chown [user]:[group] [file]` | *(Optional)* Changes the owner/group if needed. |

## 🏁 Outcome
Successfully restricted access to sensitive patient data. This aligns with the Principle of Least Privilege and mitigates the risk of internal data leaks.
echo "# Cybersecurity-Portfolio" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YourUsername/Cybersecurity-Portfolio.git
git push -u origin main
# Linux File Permissions: Securing Research Data

## 📖 Scenario
I am a security analyst at a research hospital. The lead researcher, `researcher2`, stores sensitive patient trial data in the `/home/researcher2/projects/` directory. My task was to review the current permissions and restrict unauthorized access to ensure only the `researcher2` user and the `research_team` group have access.

## 🎯 Objective
To enforce the **Principle of Least Privilege** by removing world-readable and write permissions from sensitive files, ensuring only authorized personnel can view or modify them.

## 🛠️ Tools Used
- Linux Bash Shell
- Commands: `ls -la`, `chmod`, `sudo`

---

## 🔍 Step 1: Check Current Permissions
I used `ls -la` to list all files, including hidden ones, and display the permission strings for each.

### Command Entered:
```bash
ls -la /home/researcher2/projects/
