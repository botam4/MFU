# Hướng Dẫn Flash Firmware

Hướng dẫn này bao gồm cách flash firmware cho ESP32-C3 Mini và STM32.

---

## 📦 File Cần Chuẩn Bị

### ESP32-C3 Mini
- `bootloader.bin`
- `partitions.bin`
- `firmware.bin`

### STM32
- `firmware.elf` (khuyên dùng - chứa đầy đủ thông tin)
- `firmware.hex` hoặc `firmware.bin` (thay thế)

---

## 🔧 Phần 1: ESP32-C3 Mini (ESP Flash Download Tool)

### Yêu Cầu
1. Tải **ESP Flash Download Tool** từ [Espressif](https://www.espressif.com/en/support/download/other-tools)
2. Cài driver USB (CP210x hoặc CH340 tùy board)
3. Kết nối ESP32-C3 Mini qua USB

### Hướng Dẫn Từng Bước

#### Bước 1: Mở ESP Flash Download Tool
- Chạy file `flash_download_tool_x.x.x.exe`
- Chọn **ChipType**: `ESP32-C3`
- Chọn **WorkMode**: `Develop`
- Nhấn **OK**

#### Bước 2: Cấu Hình Flash

| Cài đặt | Giá trị |
|---------|---------|
| SPI SPEED | 40MHz |
| SPI MODE | DIO |
| FLASH SIZE | 4MB (hoặc theo chip của bạn) |

#### Bước 3: Nạp File Binary

Tick vào checkbox và cấu hình từng file:

| File                 | Địa chỉ |
|------                |---------|
| ✅ `bootloader.bin` | `0x0` |
| ✅ `partitions.bin` | `0x8000` |
| ✅ `firmware.bin`   | `0x10000` |

> ⚠️ **Quan trọng**: Địa chỉ phải chính xác! Sai địa chỉ sẽ không boot được.

#### Bước 4: Chọn Cổng COM
- Chọn đúng cổng **COM** của ESP32-C3
- Đặt **BAUD** rate: `921600` (hoặc `460800` nếu không ổn định)

#### Bước 5: Vào Chế Độ Download
**Cách 1 (Tự động):** Hầu hết board tự động vào chế độ download

**Cách 2 (Thủ công):**
1. Giữ nút **BOOT**
2. Nhấn và thả nút **RESET**
3. Thả nút **BOOT**

#### Bước 6: Flash Firmware
1. Nhấn **START**
2. Chờ thanh tiến trình hoàn tất
3. Trạng thái hiển thị **FINISH**

#### Bước 7: Reset và Kiểm Tra
- Nhấn nút **RESET** hoặc rút cắm lại USB
- ESP32-C3 sẽ khởi động với firmware mới








## 🔧 Phần 2: STM32 (STM32CubeProgrammer)

### Yêu Cầu
1. Tải **STM32CubeProgrammer** từ [ST Website](https://www.st.com/en/development-tools/stm32cubeprog.html)
2. Cài đặt STM32CubeProgrammer
3. Kết nối ST-LINK V2

### Sơ Đồ Kết Nối
Kết nối ST-LINK với STM32:

| ST-LINK | STM32 |
|---------|-------|
| SWDIO | SWDIO |
| SWCLK | SWCLK |
| GND | GND |
| 3.3V | 3.3V |

### Hướng Dẫn Từng Bước

#### Bước 1: Mở STM32CubeProgrammer
- Khởi chạy **STM32CubeProgrammer**

#### Bước 2: Chọn Loại Kết Nối
- Nhấn dropdown kết nối (góc trên phải)
- Chọn **ST-LINK**

#### Bước 3: Kết Nối Thiết Bị
1. Nhấn **Connect** (biểu tượng phích cắm xanh)
2. Chờ phát hiện thiết bị
3. Trạng thái hiển thị "Connected"

#### Bước 4: Nạp File Firmware
1. Nhấn tab **Open file** (bảng bên trái)
2. Chọn file firmware:
   - **`.elf`** - Khuyên dùng, tự nhận địa chỉ
   - **`.hex`** - Tự nhận địa chỉ
   - **`.bin`** - Cần nhập **Start address**: `0x08000000`

> 💡 **Mẹo**: File `.elf` chứa đầy đủ thông tin debug và địa chỉ, STM32CubeProgrammer tự động nhận diện.

#### Bước 5: Xóa Chip (Tùy chọn nhưng khuyên dùng)
1. Vào tab **Erasing & Programming**
2. Nhấn **Full chip erase** hoặc **Sector erase**

#### Bước 6: Flash Firmware
1. Nhấn nút **Download** (biểu tượng mũi tên xuống)
2. Chờ tiến trình hoàn tất
3. Trạng thái hiển thị "File download complete"

#### Bước 7: Xác Minh (Tùy chọn)
1. Nhấn **Verify** để kiểm tra nội dung flash
2. Hiển thị "Verification OK"

#### Bước 8: Ngắt Kết Nối và Reset
1. Nhấn **Disconnect**
2. Nhấn **RESET** hoặc tắt/bật nguồn



