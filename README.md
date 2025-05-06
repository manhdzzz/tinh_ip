Đã suy nghĩ trong vài giây


Để tính dải địa chỉ (IP range) cho mạng **139.204.88.22/19**, ta làm theo các bước rất đơn giản dưới đây.

---

## 1. Hiểu rõ “/19” nghĩa là gì

* “/19” là **độ dài phần mạng** (network prefix length), tức có **19 bit** dành cho phần mạng, phần còn lại (32−19=13 bit) dành cho phần host.
* Tương đương với **subnet mask**:

  ```
  11111111.11111111.11100000.00000000
  → 255.255.224.0
  ```

---

## 2. Xác định địa chỉ mạng (Network Address)

1. Viết địa chỉ IP gốc và subnet mask ra dạng nhị phân (chỉ quan tâm đến hai octet thứ 3 để dễ hình dung):

   ```
   IP:            139   .    204   .    88    .   22
   Nhị phân: … 10001011 . 11001100 . 01011000 . 00010110
   Mask /19: … 11111111 . 11111111 . 11100000 . 00000000
   ```

2. Thực hiện phép **AND** giữa IP và mask để lấy địa chỉ mạng:

   * Octet 1,2 giống nhau (139.204).
   * Octet 3:

     ```
     01011000 (88)
     AND
     11100000 (224)
     = 01000000 (64)
     ```
   * Octet 4:

     ```
     00010110 (22)
     AND
     00000000 (0)
     = 00000000 (0)
     ```

   → **Địa chỉ mạng**: `139.204.64.0`

---

## 3. Xác định địa chỉ quảng bá (Broadcast Address)

Tính Net ID
Ta cần xác định Net ID bằng cách lấy địa chỉ IP và thực hiện phép AND với subnet mask:

IP: 139.204.88.22 = 10001011.11001100.01011000.00010110

Subnet mask: 255.255.224.0 = 11111111.11111111.11100000.00000000

AND kết quả: 10001011.11001100.01000000.00000000 → 139.204.64.0

Net ID: 139.204.64.0

Network Address:       11111111.11111111.11100000.00000000
Wildcard mask:     00000000.00000000.00011111.11111111
Net ID:                10001011.11001100.01011000.00010110
Broadcast (OR):    10001011.11001100.01011111.11111111 = 139.204.95.255


→ **Broadcast**: `139.204.95.255`

---

## 4. Dải địa chỉ host có thể cấp (Usable Hosts)

* **Host đầu tiên** (first usable): địa chỉ mạng + 1
  → `139.204.64.1`
* **Host cuối cùng** (last usable): địa chỉ broadcast − 1
  → `139.204.95.254`
* **Tổng số host khả dụng** = 2¹³ − 2 = 8190 hosts.

---


