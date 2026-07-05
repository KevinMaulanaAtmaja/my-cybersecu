# 📝 Contoh Real Life TCP/IP & OSI

---

## 🎯 Judul & Tujuan

**Topik**: Contoh Real Life TCP/IP & OSI  
**Tahap**: TAHAP-1  
**Kategori**: Networking  
**Tujuan Pembelajaran**:

- [x] Memahami Contoh Real Life TCP/IP & OSI
- [x] Mengenal komponen pembantu Lapisan TCP/IP & OSI

---

## 💡 Konsep Utama

Misal dari pc-ku akses web browser dan request ke web lain(networkchuck.coffee).
nah itu nanti dikirim ke server/pc lain dengan lewati protocol yg sama(Layer1-Layer7).

Dari pc saya:
Application-> Data, pembungkusnya disebut data
Presentation-> next materi
Session-> next materi
Transport-> Data, L4 Header(transport protocol(tcp/udp), port). pembungkusnya disebut segment
Network-> Data, L4 Header, L3 Header(src ip, dest ip). pembungkusnya disebut packet
Data Link-> L2 Trailer(FCS), Data, L4 Header, L3 Header, L2 Header(mac addrress). pembungkusnya disebut frame
Physical-> Frame dst diubah jdi (101001...) dan dari sini langsung dikirim secara fisik melalui ethernet. (101001...) disebut bits.

Setiap kali turun 1 layer disebut encasulation/dibungkus lagi dengan info baru, berhenti encapsulation hanya sampai frame.
Analoginya sperti dari menulis surat, kertas dibungkus amplop, lalu si amplop di bungkus lagi kotak dst.
setiap kali naik 1 layer disebut de-encasulated, dibuka pembungkusnya.

TCP->Reliable  
UDP->Faster

Port 443->https  
Port 90->http

**Definisi Singkat**:

>

**Visualisasi/Diagram**:

<table style="border: none; width: 100%; text-align: center;">
  <tr>
    <td style="border: none; vertical-align: top;">
      <figure>
        <img src="../../0-SOURCE/assets/4-tcp-ip-osi/3-how-data-move.png" alt="How Data Move" width="100%" style="max-height: 250px; object-fit: contain;">
        <figcaption>How Data Move</figcaption>
      </figure>
    </td>
  </tr>
</table>

---

## 📚 Sumber Belajar

| No | Sumber | Link | Format | Rating | Waktu |
|----|-----|------|--------|--------|-------|
| 1 | NetworkChuck - CCNA Course | <https://www.youtube.com/watch?v=3kfO61Mensg&list=PLIhvC56v63IJVXv0GJcl9vO5Z6znCVb1P&index=6> | Video | ⭐⭐⭐⭐⭐ | 16min |
| 2 | | | | | |
| 3 | | | | | |

**Sumber Rekomendasi**: NetworkChuck

---

## ⚡ Catatan Penting

### Poin Utama

1. **FCS(Frame Check Sequence)**: untuk mendeteksi kesalahan (error detection) saat frame dikirim.

---
