# 🔐 CONTOH-2: CIA Triad - Security Fundamental Concept

---

## 🎯 Judul & Tujuan

**Topik**: CIA Triad (Confidentiality, Integrity, Availability)  
**Tahap**: TAHAP-1  
**Kategori**: Security Fundamental / Core Concepts  
**Tujuan Pembelajaran**:
- [x] Memahami konsep CIA Triad & maknanya
- [x] Bisa explain setiap component dengan contoh real-world
- [x] Tahu implementasi CIA dalam praktik
- [x] Understand tradeoff antara CIA components
- [x] Bisa relate CIA dengan security policies

---

## 💡 Konsep Utama

CIA Triad adalah **fundamental model dalam cybersecurity** yang mendeskripsikan 3 core security objectives. Setiap keputusan security harus balance antara ketiga aspek ini.

**Definisi Singkat**:
> CIA Triad terdiri dari 3 elemen:
> - **Confidentiality**: Hanya authorized user yang bisa akses data
> - **Integrity**: Data tidak berubah atau dimodifikasi tanpa permission
> - **Availability**: Data/sistem harus accessible kapan dibutuhkan

**Visualisasi/Diagram**:
```
              ▲
             /│\
            / │ \
           /  │  \
          / C │ I \
         /____│____\
        /    │  A   \
       /     │       \
      /______________\
      
   ┌─────────────────────────────────┐
   │     CIA Triad Components        │
   ├─────────────────────────────────┤
   │ • Confidentiality (Privacy)     │
   │ • Integrity (Accuracy)          │
   │ • Availability (Accessibility)  │
   └─────────────────────────────────┘

Real-World Example:
┌──────────────────────────────────────────┐
│         Bank Account System              │
├──────────────────────────────────────────┤
│ C: Hanya user yang login bisa lihat      │
│    saldo & transaksi history             │
│                                          │
│ I: Balance tidak boleh berubah tanpa     │
│    transaksi legitimate. No corruption   │
│                                          │
│ A: Bank sistem must 24/7 operational     │
│    untuk withdraw/transfer anytime       │
└──────────────────────────────────────────┘
```

---

## 📚 Sumber Belajar

| No | Sumber | Link | Format | Rating | Waktu |
|----|--------|------|--------|--------|-------|
| 1 | Professor Messer - Security+ | https://youtu.be/[example] | Video | ⭐⭐⭐⭐⭐ | 12min |
| 2 | TryHackMe - Security Fundamentals | https://tryhackme.com/room/security101 | Interactive | ⭐⭐⭐⭐ | 30min |
| 3 | CompTIA Security+ Study Guide | Buku/PDF | Book | ⭐⭐⭐⭐ | 1h |
| 4 | NIST Cybersecurity Framework | https://www.nist.gov/cyberframework | Official Doc | ⭐⭐⭐⭐ | 45min |

**Sumber Rekomendasi**: Professor Messer - paling clear & concise explanation dengan real-world examples

---

## ⚡ Catatan Penting

### Poin Utama

#### 1. **Confidentiality (Kerahasiaan)**

**Definisi**: Protect information dari unauthorized access. Hanya authorized persons yang bisa baca data.

**Implementation**:
- Encryption (at rest & in transit)
- Access Control Lists (ACL)
- Authentication & Authorization
- Secure password policies
- VPN untuk secure communication

**Real-World Example**:
```
❌ BURUK: Password disimpan plaintext di database
   → Jika database di-hack, semua password visible

✅ BAIK: Password di-hash dengan salt
   → Even if database leaked, passwords protected
   
❌ BURUK: Email traffic tidak encrypted
   → Anyone on network bisa sniff messages

✅ BAIK: Email dengan TLS/SSL encryption
   → Communication secure & private
```

#### 2. **Integrity (Integritas)**

**Definisi**: Ensure data accurate & tidak dimodifikasi tanpa permission. Data harus tetap sama dari source ke destination.

**Implementation**:
- Hash functions (SHA-256, MD5, dll)
- Digital Signatures
- Message Authentication Code (MAC)
- Version control systems
- Data validation & error checking

**Real-World Example**:
```
❌ BURUK: File dikirim tanpa verification
   → Recipient tidak tahu apakah file modified

✅ BAIK: File + hash digenerete dari sender
   → Recipient hash file & bandingkan
   → Jika sama = integrity valid
   
❌ BURUK: Database dirubah tanpa log
   → No audit trail, no way to detect changes

✅ BAIK: Database dengan integrity checks & logs
   → Every change recorded & detectable
```

#### 3. **Availability (Ketersediaan)**

**Definisi**: Ensure systems & data accessible ketika dibutuhkan authorized users. Service harus operational.

**Implementation**:
- Redundancy & backup systems
- Load balancing
- DDoS protection
- Regular maintenance schedule
- Disaster recovery planning
- High availability architecture

**Real-World Example**:
```
❌ BURUK: Single server untuk critical service
   → Jika server down, service inaccessible

✅ BAIK: Multiple servers dengan load balancer
   → Jika 1 server down, traffic reroute ke server lain
   
❌ BURUK: No backup systems
   → Data loss berarti data hilang forever

✅ BAIK: Regular backups di multiple locations
   → Data always recoverable
```

### Tradeoff & Balancing

Seringkali ada **tension antara CIA components**:

```
Confidentiality vs Availability:
- Strict access control (C) bisa bikin slow/unavailable (A)
- Solution: Role-based access control (RBAC) yang balanced

Integrity vs Performance:
- Rigorous validation (I) bisa bikin processing slow
- Solution: Strategic validation points

Example Tradeoff:
Bank wants HIGH confidentiality (encryption), 
HIGH integrity (no data loss), 
HIGH availability (24/7).

Tapi semua ini cost money & resources!
So they need BALANCED approach.
```

### Command / Syntax (Real-World Usage)

```bash
# Confidentiality: Encrypt file
openssl enc -aes-256-cbc -in file.txt -out file.txt.enc

# Integrity: Generate hash
sha256sum file.txt > file.txt.sha256
# Verify later
sha256sum -c file.txt.sha256

# Availability: Check system status
uptime  # How long system running
free -h # Available memory
df -h   # Disk space available

# Monitoring availability
ping -c 5 8.8.8.8  # Check connectivity
```

---

## 🔬 Latihan / Praktik

### Lab Setup
```
Lokasi Lab: Conceptual + hands-on demonstration
Tools: OpenSSL, Terminal, File system
Duration: ~1-2 hours
Pre-req: Basic command line knowledge
```

### Langkah Praktik

#### Praktik 1: Confidentiality dengan Encryption

```bash
# Step 1: Create a secret file
echo "This is confidential data" > secret.txt

# Step 2: Encrypt dengan AES-256
openssl enc -aes-256-cbc -in secret.txt -out secret.txt.enc -P

# Step 3: Delete original (data only in encrypted form)
rm secret.txt

# Step 4: Try to read encrypted file
cat secret.txt.enc  # Gibberish, not readable!

# Step 5: Decrypt dengan password
openssl enc -d -aes-256-cbc -in secret.txt.enc -out secret.txt

# Step 6: Verify decrypted matches original
cat secret.txt  # Now readable again!

# Insight: Without password, encrypted file = useless (CONFIDENTIAL)
```

#### Praktik 2: Integrity dengan Hash

```bash
# Step 1: Create file
echo "Important data" > important.txt

# Step 2: Generate hash (fingerprint)
sha256sum important.txt > important.txt.sha256
cat important.txt.sha256

# Step 3: Verify integrity (should OK)
sha256sum -c important.txt.sha256  # Output: OK

# Step 4: Modify file
echo "HACKED!" >> important.txt

# Step 5: Verify again (should FAIL)
sha256sum -c important.txt.sha256  # Output: FAILED

# Insight: Hash detected modification! (INTEGRITY CHECK)
```

#### Praktik 3: Availability Monitoring

```bash
# Check system availability
uptime  # How long running without crash
free -h  # Available memory
df -h    # Disk space
systemctl status apache2  # Service running?

# If service down:
sudo systemctl start apache2  # Bring back online

# Insight: Monitoring & quick restart = maintaining AVAILABILITY
```

### Hasil & Pembelajaran

**Hasil yang diharapkan**:
1. Successful encryption/decryption = confidentiality works
2. Hash mismatch after modification = integrity detection works
3. System monitoring tools = availability awareness

**Hambatan & Solusi**:
- ❌ **Problema**: OpenSSL deprecated warnings
  - ✅ **Solusi**: Normal, still works. Update OpenSSL untuk latest version

- ❌ **Problema**: "sudo: command not found" (trying to restart service)
  - ✅ **Solusi**: Some systems need full path. Use `which systemctl` to verify

- ❌ **Problema**: Forgot encryption password
  - ✅ **Solusi**: Can't decrypt without password. This is actually GOOD (security feature)

---
