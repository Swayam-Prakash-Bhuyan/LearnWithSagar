Got it 👍 — for every task, we can add a **📸 Screenshot Placeholder** section where you’ll paste your terminal screenshots after running the commands. Here’s an updated structure of your `solution.md` with screenshot placeholders added:

---

# ✅ Daily DevOps + SRE Challenge Series – Season 2

## Day 11: The Text File Takedown – Wrangle Logs and Configs Like a Pro

### 📂 Base Setup

```bash
mkdir ~/textlab
cd ~/textlab
cat << EOF > myfile.txt
Line 1: This is a test file. Initializing systems...
Line 2: Administrator access granted. Beware of rogue agents.
Line 3: Memory usage: 500MB. System stable.
Line 4: Error log entry: Unauthorized access attempt detected.
Line 5: IP address: 192.168.1.100. Target server.
Line 6: Password: secret123. DO NOT SHARE.
Line 7: End of file. Mission critical.
EOF
```

---

## 🧩 Core Skills Training

### 1. Decoding the Intelligence

```bash
sed -n '5p' myfile.txt
awk 'NR==5' myfile.txt
```

✅ Output: `Line 5: IP address: 192.168.1.100. Target server.`

📸 **Screenshot Placeholder:**
`![Decoding the Intelligence Screenshot](screenshots/task1.png)`

---

### 2. Hunting the Target

```bash
grep -rl "192.168.1.100" ~/textlab
```

📸 **Screenshot Placeholder:**
`![Hunting the Target Screenshot](screenshots/task2.png)`

---

### 3. Reversing the Sabotage

```bash
sed -i 's/root/Administrator/' myfile.txt
```

📸 **Screenshot Placeholder:**
`![Reversing the Sabotage Screenshot](screenshots/task3.png)`

---

### 4. Memory Optimization

```bash
grep -Eo '[0-9]+MB' myfile.txt | sort -nr
```

📸 **Screenshot Placeholder:**
`![Memory Optimization Screenshot](screenshots/task4.png)`

---

### 5. System Recon

```bash
ps aux | awk '{print $6}'
```

📸 **Screenshot Placeholder:**
`![System Recon Screenshot](screenshots/task5.png)`

---

### 6. Deleting Sensitive Info

```bash
sed -i '6d' myfile.txt
```

📸 **Screenshot Placeholder:**
`![Deleting Sensitive Info Screenshot](screenshots/task6.png)`

---

## 🎯 Advanced Missions

### 1. Swapping Intel

```bash
sed -n '1,2p;4p;3p;5,$p' myfile.txt > tmp && mv tmp myfile.txt
```

📸 **Screenshot Placeholder:**
`![Swapping Intel Screenshot](screenshots/task7.png)`

---

### 2. Archiving Enemy Logs

```bash
find ~/textlab/logs -name "*.log" -size +1M -print
tar -czvf logs_archive.tar.gz ~/textlab/logs/log1.log
```

📸 **Screenshot Placeholder:**
`![Archiving Enemy Logs Screenshot](screenshots/task8.png)`

---

### 3. Finding Patterns

```bash
grep -i "error" ~/textlab/logs/log1.log | tr '[:space:]' '\n' | sort | uniq -c
```

📸 **Screenshot Placeholder:**
`![Finding Patterns Screenshot](screenshots/task9.png)`

---

### 4. Alerting the Team

```bash
grep --color=always -r "password" ~/textlab
grep -r "password" ~/textlab | mail -s "⚠️ ALERT: Password Found" you@example.com
```

📸 **Screenshot Placeholder:**
`![Alerting the Team Screenshot](screenshots/task10.png)`

---

## 📌 Submission

* Save as `solution.md`.
* Place screenshots in `screenshots/` folder.
* Update each placeholder with your actual file path.
* Push to GitHub.

---

