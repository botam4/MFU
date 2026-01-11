# How to Flash Firmware

This guide covers flashing firmware for both ESP32-C3 Mini and STM32 microcontrollers.

---

## 📦 Required Files

### ESP32-C3 Mini
- `bootloader.bin`
- `partitions.bin`
- `firmware.bin`

### STM32
- `firmware.hex` or `firmware.bin` or `firmware.elf`

---

## 🔧 Part 1: ESP32-C3 Mini (ESP Flash Download Tool)

### Prerequisites
1. Download **ESP Flash Download Tool** from [Espressif](https://www.espressif.com/en/support/download/other-tools)
2. Install USB driver (CP210x or CH340 depending on your board)
3. Connect ESP32-C3 Mini via USB

### Step-by-Step Instructions

#### Step 1: Open ESP Flash Download Tool
- Run `flash_download_tool_x.x.x.exe`
- Select **ChipType**: `ESP32-C3`
- Select **WorkMode**: `Develop`
- Click **OK**

#### Step 2: Configure Flash Settings

| Setting | Value |
|---------|-------|
| SPI SPEED | 40MHz |
| SPI MODE | DIO |
| FLASH SIZE | 4MB (or match your chip) |

#### Step 3: Load Binary Files

Check the checkbox and configure each file:

| File | Address |
|------|---------|
| ✅ `bootloader.bin` | `0x0` |
| ✅ `partitions.bin` | `0x8000` |
| ✅ `firmware.bin` | `0x10000` |

> ⚠️ **Important**: Addresses must be exact! Wrong addresses will cause boot failure.

#### Step 4: Select COM Port
- Choose the correct **COM** port for your ESP32-C3
- Set **BAUD** rate to `921600` (or `460800` if unstable)

#### Step 5: Enter Download Mode
**Method 1 (Auto):** Most boards auto-enter download mode

**Method 2 (Manual):**
1. Hold **BOOT** button
2. Press and release **RESET** button
3. Release **BOOT** button

#### Step 6: Flash Firmware
1. Click **START**
2. Wait for progress bar to complete
3. Status should show **FINISH**

#### Step 7: Reset and Verify
- Press **RESET** button or reconnect USB
- ESP32-C3 should boot with new firmware








## 🔧 Part 2: STM32 (STM32CubeProgrammer)

### Prerequisites
1. Download **STM32CubeProgrammer** from [ST Website](https://www.st.com/en/development-tools/stm32cubeprog.html)
2. Install STM32CubeProgrammer
3. Connect ST-LINK V2

### Connection Methods
Connect ST-LINK to STM32:

| ST-LINK | STM32 |
|---------|-------|
| SWDIO | SWDIO |
| SWCLK | SWCLK |
| GND | GND |
| 3.3V | 3.3V |

### Step-by-Step Instructions

#### Step 1: Open STM32CubeProgrammer
- Launch **STM32CubeProgrammer**

#### Step 2: Select Connection Type
- Click connection dropdown (top right)
- Select **ST-LINK** 

#### Step 3: Connect to Device
1. Click **Connect** (green plug icon)
2. Wait for device detection
3. Status should show "Connected"

#### Step 4: Load Firmware File
1. Click **Open file** tab (left panel)
2. Browse and select `firmware.hex` or `firmware.bin` or `firmware.elf`
3. For `.bin` files, set **Start address**: `0x08000000`

#### Step 5: Erase Chip (Optional but Recommended)
1. Go to **Erasing & Programming** tab
2. Click **Full chip erase** or **Sector erase**

#### Step 6: Flash Firmware
1. Click **Download** button (arrow down icon)
2. Wait for progress to complete
3. Status shows "File download complete"

#### Step 7: Verify (Optional)
1. Click **Verify** to check flash content
2. Should show "Verification OK"

#### Step 8: Disconnect and Reset
1. Click **Disconnect**
2. Press **RESET** or power cycle


