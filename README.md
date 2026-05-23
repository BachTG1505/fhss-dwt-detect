# FHSS-DWT Detect

Bài thực hành Labtainers khảo sát kỹ thuật steganalysis cho hệ thống giấu tin âm thanh sử dụng DWT kết hợp FHSS và QIM.

---

## Mục tiêu

Sinh viên đóng vai trò nhà phân tích an toàn thông tin để kiểm tra một file âm thanh có chứa dữ liệu giấu hay không.

Bài lab cho thấy:

- Các phương pháp quan sát phổ thông thường có thể không phát hiện được steganography
- DWT-FHSS-QIM tạo thay đổi rất nhỏ trên phổ tín hiệu
- Phân tích trực tiếp miền wavelet và thống kê QIM hiệu quả hơn trong phát hiện dữ liệu ẩn

Sinh viên sẽ:

- Quan sát spectrogram bằng Sonic Visualiser
- Phân tích năng lượng tín hiệu
- So sánh hệ số DWT
- Thực hiện kiểm định thống kê QIM
- Đưa ra kết luận steganalysis

---

## Tải bài lab

```bash
imodule https://github.com/BachTG1505/fhss-dwt-detect/raw/main/fhss-dwt-detect.tar
```

---

## Khởi động bài lab

```bash
cd ~/labtainer/trunk/scripts/labtainer-student

labtainer -r fhss-dwt-detect
```

---

## Các task

### Task 1 - Setup dữ liệu

```bash
python3 setup_lab.py
```

Script thực hiện:

- Tạo `stego_audio.wav`
- Nhúng thông điệp `HELLO PTIT!`
- Sử dụng kỹ thuật DWT-FHSS-QIM
- Hiển thị chỉ số PSNR

Kết quả mong đợi:

```text
PSNR ≈ 80-90 dB
```

Âm thanh stego gần như không khác biệt cảm thụ so với audio gốc.

---

### Task 2 - Quan sát bằng Sonic Visualiser

```bash
sonic-visualiser stego_audio.wav &
```

Trong Sonic Visualiser:

```text
Layer -> Add Spectrogram
```

Quan sát:

- Phổ tín hiệu
- Vệt tần số
- Dấu hiệu bất thường

Kết luận mong đợi:

```text
KHÔNG phát hiện dấu hiệu rõ ràng
```

DWT-FHSS-QIM không tạo các vạch tần số nổi bật như FHSS truyền thống.

---

### Task 3 - Energy Analysis

```bash
python3 energy_analysis.py

cat energy_report.txt
```

Script tính năng lượng theo các band tần số khác nhau.

Mục tiêu:

- Kiểm tra thay đổi năng lượng phổ
- Phát hiện band bất thường

Kết luận mong đợi:

```text
Không phát hiện band năng lượng bất thường
```

Phương pháp energy analysis không đủ nhạy với DWT-FHSS-QIM.

---

### Task 4 - DWT Difference Analysis

```bash
python3 dwt_diff_analysis.py

cat dwt_report.txt
```

Script thực hiện:

- DWT trên audio gốc và audio stego
- So sánh hệ số wavelet
- Tìm dấu vết thay đổi do QIM gây ra

Kết luận mong đợi:

```text
DWT difference detected
```

Đây là phương pháp hiệu quả khi có audio gốc để đối chiếu.

---

### Task 5 - Blind Statistical Analysis

```bash
python3 statistical_analysis.py

cat stats_report.txt
```

Script phân tích:

- Phân bố modulo DELTA
- Thống kê hệ số wavelet
- Kiểm định chi-square QIM

Nếu nhiều sub-band có chi-square cao:

```text
Suspicious QIM distribution detected
```

Đây là phương pháp blind steganalysis vì không cần audio gốc.

---

### Task 6 - Detection Summary

```bash
python3 detection_summary.py

cat detection_summary.txt
```

Kết quả cuối cùng mong đợi:

```text
STEGANOGRAPHY DETECTED
```

---

## Kết luận chính

### Spectrogram Analysis

Spectrogram khó phát hiện DWT-FHSS-QIM vì:

- Dữ liệu được nhúng trong hệ số wavelet
- Thay đổi phân tán
- Không tạo vạch tần số mạnh

### Energy Analysis

Energy analysis theo band rộng:

- Không đủ nhạy
- Khó phát hiện biến đổi nhỏ do QIM

### DWT Difference

DWT Difference:

- Hiệu quả nếu có audio gốc
- Phát hiện trực tiếp thay đổi wavelet coefficient

### Blind Statistical Analysis

Chi-square QIM:

- Có ý nghĩa thực tế hơn
- Không cần audio gốc
- Phát hiện phân bố bất thường của hệ số wavelet

---

## Công cụ sử dụng

- Python 3
- NumPy
- PyWavelets
- Sonic Visualiser
- Labtainers

---

## Kiến thức đạt được

- Audio steganalysis
- DWT Haar transform
- FHSS-QIM steganography
- Wavelet coefficient analysis
- Chi-square statistical detection
- Blind steganalysis
- Spectrum analysis

---

## Tác giả

- Họ tên: **Trương Gia Bách**
- Mã sinh viên: **B22DCAT024**
- Học phần: **INT14102 - Kỹ thuật giấu tin**
- Học viện Công nghệ Bưu chính Viễn thông

