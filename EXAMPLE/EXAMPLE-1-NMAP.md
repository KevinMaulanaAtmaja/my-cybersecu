# 🔍 CONTOH-1: Nmap - Network Mapper Tool

---

## 🎯 Judul & Tujuan

**Topik**: Nmap (Network Mapper)  
**Tahap**: TAHAP-2  
**Kategori**: Red Team / Reconnaissance Tools  
**Tujuan Pembelajaran**:
- [x] Memahami apa itu Nmap dan fungsinya
- [x] Mengenal berbagai scan type (-sS, -sV, -sC, dll)
- [x] Bisa perform basic port scanning
- [x] Membaca & interpret Nmap output
- [x] Praktik scan pada VM lokal

---

## 💡 Konsep Utama

Nmap adalah **free open-source tool** untuk network exploration dan security auditing. Alat ini digunakan untuk discover hosts & services dalam network, map network topology, dan identify open ports.

**Definisi Singkat**:
> Nmap (Network Mapper) adalah tools untuk scan port, detect OS, dan identify services running pada target machine. Fundamental skill untuk penetration tester dan network administrator.

**Visualisasi/Diagram**:
```
┌─────────────────────────────────────────┐
│        Nmap Workflow                    │
├─────────────────────────────────────────┤
│                                         │
│  Target IP/Network                      │
│       ↓                                  │
│  [Nmap Scan]                            │
│       ↓                                  │
│  ├─ Host Discovery                      │
│  ├─ Port Scanning                       │
│  ├─ Service Detection                   │
│  └─ OS Fingerprinting                   │
│       ↓                                  │
│  Output → Analysis                      │
│                                         │
└─────────────────────────────────────────┘

Basic Scan Progression:
Ping Sweep → Port Scan → Service Detection → OS Detection
(Finding hosts) → (Open ports) → (What's running) → (Which OS)
```

---

## 📚 Sumber Belajar

| No | Sumber | Link | Format | Rating | Waktu |
|----|--------|------|--------|--------|-------|
| 1 | TryHackMe - Nmap Tutorial | https://tryhackme.com/room/nmap | Interactive | ⭐⭐⭐⭐⭐ | 1.5h |
| 2 | John Hammond - Nmap Basics | https://youtu.be/[example] | Video | ⭐⭐⭐⭐ | 45min |
| 3 | Nmap Official Documentation | https://nmap.org/docs.html | Documentation | ⭐⭐⭐⭐ | 2h |
| 4 | IppSec - Nmap Deep Dive | https://youtu.be/[example] | Video | ⭐⭐⭐⭐⭐ | 1h |

**Sumber Rekomendasi**: TryHackMe Nmap room - paling interactive & comprehensive

---

## ⚡ Catatan Penting

### Poin Utama

1. **Port Scanning Types**:
   - **-sS** (SYN Scan): Stealthy, tidak complete 3-way handshake, faster
   - **-sT** (Connect Scan): Complete handshake, slower, lebih mudah dideteksi
   - **-sU** (UDP Scan): Scan UDP ports, lebih lambat
   - **-p-** (All Ports): Scan semua 65535 port

2. **Service Detection**:
   - **-sV**: Detect service version running pada open ports
   - **-sC**: Menggunakan default NSE scripts untuk additional info
   - **-O**: Detect operating system (butuh root privilege)

3. **Output Formats**:
   - **-oN**: Normal output (plain text)
   - **-oX**: XML output (untuk parsing)
   - **-oA**: Output semua format sekaligus

4. **Port States** (important!):
   - **Open**: Service listening & accessible
   - **Closed**: Port accessible tapi tidak ada service (firewall allow)
   - **Filtered**: Port tidak accessible (firewall block)
   - **Unfiltered**: Port accessible tapi status unclear
   - **Open|Filtered**: Open atau filtered (ambiguous)
   - **Closed|Filtered**: Closed atau filtered

### Command / Syntax

```bash
# Basic scan (most common)
nmap -sV -sC -oN output.txt 192.168.56.101

# Aggressive scan (lebih in-depth)
nmap -A -p- -oA results 192.168.56.101

# SYN Scan (stealthy, requires root)
sudo nmap -sS -p 1-1000 192.168.56.101

# Scan specific port range
nmap -p 20-25,80,443 192.168.56.101

# Scan dengan timing template (0-5, 5=most aggressive)
nmap -T4 -p- 192.168.56.101

# Version detection + NSE scripts
nmap -sV -sC --script=vuln 192.168.56.101

# OS Detection (requires root)
sudo nmap -O 192.168.56.101

# Scan subnet
nmap -sn 192.168.56.0/24  # Ping sweep
nmap -p- 192.168.56.0/24  # Scan semua host & ports
```

---

## 🔬 Latihan / Praktik

### Lab Setup
```
Lokasi Lab: VirtualBox VM (Linux target)
Target IP: 192.168.56.101
Duration: ~45 minutes
Tools: nmap (installed on attacker machine)
Pre-req: Attacker & target VM running in same network
```

### Langkah Praktik

1. **Setup & Verification**
   - Ensure target VM is running
   - Ping target: `ping 192.168.56.101`
   - Confirm connectivity (should get reply)

2. **Basic Port Scan**
   ```bash
   nmap -p- 192.168.56.101
   # Lihat semua open ports
   ```

3. **Detailed Service Scan**
   ```bash
   nmap -sV -sC 192.168.56.101
   # Detect service + version + run scripts
   ```

4. **Full Aggressive Scan**
   ```bash
   nmap -A 192.168.56.101
   # Combine OS detection + version + script + traceroute
   ```

5. **Scan Specific Services**
   ```bash
   nmap -p 22,80,443 -sV 192.168.56.101
   # Focus only pada port SSH, HTTP, HTTPS
   ```

### Hasil & Pembelajaran

**Hasil yang diharapkan**:
```
Nmap scan report for 192.168.56.101
Host is up (0.0045s latency).
Not shown: 997 filtered ports
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.4 (protocol 2.0)
80/tcp  open  http    Apache httpd 2.4.6
111/tcp open  rpcbind 2-4 (RPC #100000)

OS fingerprint results:
...
```

**Hambatan & Solusi**:
- ❌ **Problema**: "nmap: command not found"
  - ✅ **Solusi**: Install nmap dulu: `sudo apt install nmap`

- ❌ **Problema**: "All ports showing as filtered"
  - ✅ **Solusi**: Target mungkin punya firewall aggressive atau timing template terlalu lambat. Coba T4: `nmap -T4 -sV target`

- ❌ **Problema**: SYN scan requires root
  - ✅ **Solusi**: Gunakan `sudo` untuk privileged scans: `sudo nmap -sS target`

---
