Đã suy nghĩ trong giây lát


Để bạn – người mới bắt đầu – dễ hình dung, mình sẽ chia làm 4 bước chính:

1. **Xác định mặt nạ mạng (subnet mask) từ “/19”**
2. **Chuyển địa chỉ IP về dạng nhị phân**
3. **Tính địa chỉ mạng (network address) và địa chỉ quảng bá (broadcast address)**
4. **Xác định dải IP khả dụng (usable hosts)**

---

## 1. Xác định subnet mask của /19

* `/19` nghĩa là có **19 bit** dành cho phần mạng (network), còn lại 13 bit cho phần host.
* Mặt nạ mạng (decimal) sẽ là:

  | Octet thứ | 1        | 2        | 3        | 4        |
  | --------- | -------- | -------- | -------- | -------- |
  | Bit mask  | 8 bit    | 8 bit    | 3 bit    | 0 bit    |
  | Nhị phân  | 11111111 | 11111111 | 11100000 | 00000000 |
  | Thập phân | 255      | 255      | 224      | 0        |

**Kết luận:** subnet mask = **255.255.224.0**

---

## 2. Chuyển IP 139.204.88.22 về nhị phân

| Octet     | Giá trị thập phân | Nhị phân |
| --------- | ----------------- | -------- |
| 1st (139) | 139               | 10001011 |
| 2nd (204) | 204               | 11001100 |
| 3rd (88)  | 88                | 01011000 |
| 4th (22)  | 22                | 00010110 |

Vậy IP nhị phân:

```
10001011 . 11001100 . 01011000 . 00010110
```

---

## 3. Tính Network và Broadcast

### 3.1. Network Address

* Giữ nguyên **19 bit** đầu của IP, các bit còn lại (13 bit) đặt =0.

  * Hai octet đầu (16 bit) giữ nguyên:

    ```
    10001011 . 11001100  → 139 . 204
    ```
  * Trong octet thứ 3, giữ 3 bit đầu, 5 bit sau đặt 0:

    ```
    01011000  
    → chỉ lấy 3 bit đầu: 010  
    → nối 5 bit 0: 01000000  = 64
    ```
  * Octet thứ 4 toàn bộ =0.

* **Network address** = **139.204.64.0**

### 3.2. Broadcast Address

* Broadcast = Network + (số host trong mạng) – 1.

* Số host trong /19 = 2⁽³²–19⁾ = 2¹³ = 8192 địa chỉ.

* Nhưng chúng ta cộng tới địa chỉ cuối trong khối, tức cộng 8192–1 = 8191.

* Cách đơn giản hơn:

  * Khoảng nhảy (block size) ở octet 3 = 256 – 224 = 32 → mạng bắt đầu tại 0,32,64,96,…
  * Mạng của chúng ta bắt đầu ở 64 → kết thúc ở 64+32–1 = 95.
  * Octet 4 = 255.

* **Broadcast address** = **139.204.95.255**

---

## 4. Dải IP khả dụng (Usable Hosts)

* **First usable** (địa chỉ đầu tiên dùng cho host) = Network + 1 = **139.204.64.1**
* **Last usable** (địa chỉ cuối cùng dùng cho host) = Broadcast – 1 = **139.204.95.254**
* **Tổng số host khả dụng** = 2¹³ – 2 = **8190** (bỏ network và broadcast)

---

### Tóm tắt kết quả

| Thông số          | Địa chỉ        |
| ----------------- | -------------- |
| Subnet mask (/19) | 255.255.224.0  |
| Network address   | 139.204.64.0   |
| Broadcast address | 139.204.95.255 |
| First usable host | 139.204.64.1   |
| Last usable host  | 139.204.95.254 |
| Số host khả dụng  | 8.190          |

---
