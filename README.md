# 🎥 Raspberry Pi Camera System
## Professional Technical Documentation and Hardware Compatibility Document

* **Version:** 2.0
* **Date:** January 2026
* **Platform:** Raspberry Pi 4 Model B (8GB RAM)

---

## 📺 YouTube Video Series (Step-by-Step Build)
This technical documentation covers the entire development of the Shutter Pi project. You can watch the full build and engineering journey on YouTube:

| Episode | Content Description | Status | Watch Link |
| :--- | :--- | :--- | :--- |
| **🎥 Part 1** | Build Your Own Raspberry Pi Camera! First Look | 🚀 Live | [Watch on YouTube](https://youtu.be/DRP7rBsVmwo) |
| **🔧 Part 2** | Raspberry Pi Camera Build – Hardware Assembly | ⏳ Coming Soon | [Watch on YouTube](https://youtu.be/vsTkTUwmtEQ) |
| **💻 Part 3** | Raspberry Pi Camera – App Setup & Field test | ⏳ Coming Soon | [Watch on YouTube](https://youtube.com) |

---

## 📋 Hardware Configuration
### Main System Components

| Component | Model / Specification | Status |
| :--- | :--- | :--- |
| **Main Board** | Raspberry Pi 4 Model B – 8GB RAM | ✅ Active |
| **Power Management** | UPS HAT (B) Module | ✅ Active |
| **Camera Module** | Arducam IMX477 HQ Camera (12.3MP, 1/2.3") | ✅ Active |
| **Display** | WaveShare 4.3" DSI Capacitive Touch (800×480) | ✅ Active |
| **LED Lighting** | 3W LED Module (Flash / Continuous Light) | ✅ Active |

---

## 🖥️ Raspberry Pi 4 Model B (8GB)
### Technical Specifications

| Feature | Value |
| :--- | :--- |
| **Processor** | Broadcom BCM2711, Quad-core Cortex-A72 (ARM v8) @ 1.8GHz |
| **RAM** | 8GB LPDDR4-3200 SDRAM |
| **GPU** | VideoCore VI (OpenGL ES 3.1, Vulkan 1.0) |
| **Video Output** | 2× micro-HDMI (4Kp60), DSI display port |
| **Camera Interface** | 2-lane MIPI CSI camera port |
| **USB** | 2× USB 3.0, 2× USB 2.0 |
| **Network** | Gigabit Ethernet, Wi-Fi 802.11ac, Bluetooth 5.0 |
| **GPIO** | 40-pin GPIO header |

### Application Compatibility

| Feature | Performance | Notes |
| :--- | :--- | :--- |
| **Camera Preview** | 30+ FPS | Full performance |
| **Face Detection** | Real-time | OpenCV Haar Cascade |
| **4K Video Recording** | ✅ Supported | H.264 hardware encoding |
| **LUT Filter Processing**| Smooth | Advantage of 8GB RAM |
| **Multitasking** | Excellent | Simultaneous recording + preview |

---

## 🔋 UPS HAT (B) Module
### General Information
The UPS HAT (B) is an uninterruptible power supply module designed for Raspberry Pi. It allows the system to continue operating during power outages, preventing data loss and ensuring safe shutdown or uninterrupted recording.

### Technical Specifications
* **Battery Type:** 2× 18650 Li-ion *(not included)*
* **Output Voltage:** 5V (regulated)
* **Output Current:** 2.5A (maximum)
* **Communication:** I2C interface
* **Mounting:** Plugs directly onto 40-pin GPIO header

### Application Integration
The camera system gains the following advantages when used with the UPS HAT:
* **Sudden Power Loss Protection:** Video recordings are safely finalized during outages.
* **Power Management:** Low-battery warnings can be displayed to the user.
* **Mobile Operation:** Enables portable, cable-free usage.
* **Battery Status Monitoring:** Real-time charge and discharge information.

> 📌 **Note:** Battery status data is read via the I2C interface and forwarded to the `BatteryNativeWidget` component.

---

## 📷 Arducam IMX477 HQ Camera Module
### General Information
The high-quality camera module featuring the Sony IMX477 sensor delivers professional-grade image quality. It uses the same sensor as the official Raspberry Pi HQ Camera module and is fully compatible with advanced imaging applications.

### Technical Specifications
| Feature | Value |
| :--- | :--- |
| **Sensor** | Sony IMX477 |
| **Resolution** | 12.3 Megapixels |
| **Sensor Size** | 1/2.3 inch (7.9mm diagonal) |
| **Pixel Size** | 1.55 μm × 1.55 μm |
| **Maximum Image** | 4056 × 3040 pixels |
| **Video Modes** | 1080p60, 4K30 |
| **Lens Mount** | C/CS-Mount or M12 |
| **Interface** | 2-lane MIPI CSI-2 |

### Supported Resolutions
| Mode | Resolution | FPS | Use Case |
| :--- | :--- | :--- | :--- |
| **Full Resolution**| 4056 × 3040 | 10 | High-quality photography |
| **4K Video** | 3840 × 2160 | 30 | Video recording |
| **Full HD** | 1920 × 1080 | 60 | Standard video |
| **HD** | 1280 × 720 | 90 | High-FPS video |
| **Preview** | 640 × 480 | 90+ | Live preview |

### Application Integration
`LibcameraCameraWorker` Configuration tree:
```text
├── Preview Stream: 640×480 @ 30 FPS (lores stream)
├── Recording Stream: 1920×1080 @ 30 FPS (main stream)
├── Photo Capture: 4056×3040 (sensor maximum)
└── 4K Mode: 3840×2160 @ 30 FPS (optional)
