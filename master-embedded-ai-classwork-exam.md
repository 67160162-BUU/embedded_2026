# 🎓 Master Embedded AI: สรุปบทเรียน + งานใน Class + เปรียบเทียบ YOLOv4 vs v5 + คลังข้อสอบ (ฉบับสมบูรณ์ชุดเดียวจบ)

> **รหัสวิชา**: 89037467 (Introduction to Embedded AI) | ผู้สอน: อ.ดร.พลวัต ช่อผูก  
> **ฉบับบูรณาการสมบูรณ์**: รวมการติดตั้ง OS & การใช้งาน RPI + การวิเคราะห์เปรียบเทียบบอร์ดทั้ง 8 ตัว + สถาปัตยกรรมบัส + การคำนวณมือ CNN/MLP + กลไก 5 เลเยอร์ LLM + **เจาะลึกผังโครงสร้างสถาปัตยกรรม YOLOv4 vs YOLOv5 จากบันทึกในชั้นเรียน** + คลังข้อสอบปรนัย (ข้อกา 20 ข้อ) และอัตนัย (ข้อเขียน 6 ข้อใหญ่พร้อมวิธีทำละเอียด)

---

# 📑 สารบัญเนื้อหา

1. [ส่วนที่ 1: การใช้งานและการติดตั้ง OS บน Raspberry Pi (RPI)](#ส่วนที่-1-การใช้งานและการติดตั้ง-os-บน-raspberry-pi-rpi)
2. [ส่วนที่ 2: สถาปัตยกรรมคอมพิวเตอร์, ระบบบัส & การคำนวณหน่วยความจำ](#ส่วนที่-2-สถาปัตยกรรมคอมพิวเตอร์-ระบบบัส--การคำนวณหน่วยความจำ)
3. [ส่วนที่ 3: Deep Learning, CNN & การคำนวณโครงสร้างด้วยมือ (จาก Lab 3, 4 และใน Class)](#ส่วนที่-3-deep-learning-cnn--การคำนวณโครงสร้างด้วยมือ)
4. [ส่วนที่ 4: กลไก 5 เลเยอร์หลักของ LLM และการปรับใช้บน Edge (จาก Week 2)](#ส่วนที่-4-กลไก-5-เลเยอร์หลักของ-llm-และการปรับใช้บน-edge)
5. [ส่วนที่ 5: เจาะลึกผังโครงสร้างสถาปัตยกรรม YOLOv4 vs YOLOv5 (จากบันทึกใน Class Week 6)](#ส่วนที่-5-เจาะลึกผังโครงสร้างสถาปัตยกรรม-yolov4-vs-yolov5)
6. [ส่วนที่ 6: กรณีศึกษาระบบตรวจจับ PPE บน Raspberry Pi 4 และโมเดล Edge อื่นๆ](#ส่วนที่-6-กรณีศึกษาระบบตรวจจับ-ppe-บน-raspberry-pi-4-และโมเดล-edge-อื่นๆ)
7. [ส่วนที่ 7: การวิเคราะห์และเปรียบเทียบบอร์ด Edge AI ทั้ง 8 ตัว (จากรูปสเปกฮาร์ดแวร์)](#ส่วนที่-7-การวิเคราะห์และเปรียบเทียบบอร์ด-edge-ai-ทั้ง-8-ตัว)
8. [🎯 คลังข้อสอบจำลอง: ชุดข้อสอบปรนัย (ข้อกา 20 ข้อ พร้อมเฉลยละเอียด)](#-คลังข้อสอบจำลอง-ชุดข้อสอบปรนัย-ข้อกา-20-ข้อ)
9. [✍️ คลังข้อสอบจำลอง: ชุดข้อสอบอัตนัย (ข้อเขียน 6 ข้อใหญ่ แสดงวิธีทำจริง)](#️-คลังข้อสอบจำลอง-ชุดข้อสอบอัตนัย-ข้อเขียน-6-ข้อใหญ่)

---

# ส่วนที่ 1: การใช้งานและการติดตั้ง OS บน Raspberry Pi (RPI)

*(อ้างอิง: คู่มือ Raspberry Pi 4 เบื้องต้น, ใบงานสัปดาห์ที่ 5 และรายงานระบบ PPE)*

### 1.1 ขั้นตอนการติดตั้ง Raspberry Pi OS (Flash & First-Boot)
1. **เครื่องมือมาตรฐาน**: ใช้โปรแกรม **Raspberry Pi Imager** (รองรับ Windows, macOS, Linux)
2. **การตั้งค่า (Settings ใน Imager)**:
   * **Choose Device**: เลือกรุ่นบอร์ดให้ตรง (เช่น Raspberry Pi 4 หรือ Raspberry Pi 5)
   * **Choose OS**: เลือกระบบปฏิบัติการ เช่น:
     * *Raspberry Pi OS (64-bit)*: แนะนำสำหรับการรัน Deep Learning, Docker และไลบรารี 64-bit ยุคใหม่
     * *Raspberry Pi OS Lite (64-bit)*: ไม่มี GUI Desktop ประหยัด RAM เหมาะกับงาน Server/IoT
   * **Choose Storage**: เลือก MicroSD Card ขนาดอย่างน้อย 16 GB (แนะนำความเร็ว Class 10 หรือ A1/A2) หรือ NVMe SSD (ผ่านบอร์ด M.2 HAT บน Pi 5)
3. **OS Customization (หัวใจสำคัญของการเซ็ตอัปแบบ Headless)**:
   * กดปุ่ม **EDIT SETTINGS** ล่วงหน้าก่อนเขียนข้อมูล:
     * ตั้งชื่อ **Hostname** (เช่น `raspberrypi.local`)
     * กำหนด **Username & Password** ของระบบ
     * ตั้งค่า **Wi-Fi** (SSID และ Password) และเลือก Timezone เป็น `Asia/Bangkok`
     * **เปิดใช้งาน SSH (Secure Shell)**: อยู่ในแถบ Services เพื่อให้เชื่อมต่อควบคุมระยะไกลได้ทันทีโดยไม่ต้องต่อจอภาพ คีย์บอร์ด หรือเมาส์
4. **การเชื่อมต่อและเปิดเครื่องครั้งแรก**:
   * เสียบสายตามลำดับ: สายสัญญาณภาพ (ถ้ามี) $\to$ สาย LAN (ถ้าใช้) $\to$ **เสียบอะแดปเตอร์ไฟเป็นขั้นตอนสุดท้ายเสมอ**
   * เชื่อมต่อผ่าน Terminal: `ssh username@raspberrypi.local`

### 1.2 กฎเหล็กการต่อสายและระบบจอภาพ (ออกสอบบ่อย)
* **การต่อจอ micro-HDMI**: บอร์ด Raspberry Pi 4 มี 2 พอร์ต **ต้องเสียบช่อง micro-HDMI 0 (ช่องที่อยู่ชิดกับพอร์ตจ่ายไฟ USB-C) เป็นพอร์ตหลัก** หากเสียบช่อง HDMI 1 จอภาพอาจไม่แสดงผลตอนเริ่มบูตระบบ
* **ระบบจัดการจอภาพแบบใหม่ (KMS)**: ปัจจุบันระบบใช้ไดรเวอร์ **Kernel Modesetting (KMS)** ทำให้การเข้าไปแก้ค่า `hdmi_group` หรือ `hdmi_mode` ในไฟล์ `config.txt` **ไม่มีผลอีกต่อไป** (ต้องปรับผ่าน Screen Configuration หรือตั้ง Headless Resolution)
* ⚠️ **กฎเหล็กของ `cmdline.txt`**: ข้อความคำสั่งในไฟล์ `cmdline.txt` **ต้องเขียนให้อยู่ในบรรทัดเดียวเท่านั้น ห้ามขึ้นบรรทัดใหม่เด็ดขาด** หากขึ้นบรรทัดใหม่ เครื่องจะไม่สามารถบูตระบบปฏิบัติการได้

### 1.3 คำสั่งพื้นฐานและคำสั่งตั้งค่าระบบที่จำเป็น
* **อัปเดตระบบ**:
  ```bash
  sudo apt update && sudo apt full-upgrade -y
  ```
* **ยูทิลิตี้ตั้งค่าฮาร์ดแวร์ (`raspi-config`)**:
  ```bash
  sudo raspi-config
  ```
  * *Interface Options*: เปิด/ปิด I2C, SPI, UART, Camera (CSI), Serial, Remote GPIO
  * *System Options*: เปลี่ยนรหัสผ่าน, เชื่อมต่อเครือข่าย, Boot Mode (Console/Desktop)
  * *Advanced Options*: Expand Filesystem (ขยายพาร์ติชันให้เต็มความจุการ์ด)
* **การเปิดใช้ Virtual Keyboard (คีย์บอร์ดบนหน้าจอ)**:
  * ใน Raspberry Pi OS รุ่นปัจจุบัน ใช้โปรแกรมมาตรฐานชื่อ **Squeekboard**
  * คำสั่งติดตั้ง: `sudo apt update && sudo apt install squeekboard && sudo reboot`
  * (หมายเหตุ: บน Wayland สามารถใช้ `wvkbd` ส่วนบน X11 ใช้ `matchbox-keyboard`)
* **การตรวจสอบสถานะฮาร์ดแวร์**:
  ```bash
  vcgencmd measure_temp      # เช็คอุณหภูมิ CPU (°C)
  vcgencmd get_throttled      # เช็คสถานะไฟตก (Undervoltage) หรือความร้อนเกิน (Throttled)
  free -h                     # เช็คการใช้งาน RAM และ Swap
  df -h                       # เช็คพื้นที่ความจุ Storage
  htop                        # ดูภาระงาน CPU แยกรายคอร์
  ```

### 1.4 การควบคุมพอร์ต GPIO (General Purpose Input/Output)
* **พิน GPIO บน RPI (40 พิน)**:
  * แรงดันลอจิกเป็น **3.3V ห้ามป้อน 5V เข้าขา GPIO ตรงๆ** มิฉะนั้นชิป SoC จะเสียหายถาวรทันที
  * มีบัสสื่อสารในตัว: I2C (SDA, SCL), SPI (MOSI, MISO, SCLK, CE), UART (TX, RX), PWM
* **การเขียนโค้ด Python ควบคุม (ใช้ไลบรารี `gpiozero` บน Bookworm)**:
  ```python
  from gpiozero import LED, Button
  from time import sleep

  led = LED(17)        # ขา GPIO 17
  button = Button(2)   # ขา GPIO 2 (มี Internal Pull-up)

  while True:
      if button.is_pressed:
          led.on()
      else:
          led.off()
      sleep(0.1)
  ```

### 1.5 การจัดการความร้อน (Thermal Management & Throttling)
* **พฤติกรรมความร้อน**: บอร์ด Raspberry Pi 4 เริ่มเกิดสภาวะ **Thermal Throttling เมื่ออุณหภูมิแตะ ~80°C**
* หากไม่มีพัดลมระบายความร้อน เมื่อรันโมเดล AI หนักๆ อุณหภูมิจะพุ่งแตะ **85°C ภายในเวลาเพียง 50 วินาที** ส่งผลให้ CPU ลดสัญญาณนาฬิกาลง ทำให้ Throughput ของระบบ**ลดลงมากกว่า 35%**
* **แนวทางแก้ไข**: ติดตั้งพัดลมระบายความร้อนแบบ Active Cooling โดยควบคุมแบบ Hysteresis ที่ช่วงอุณหภูมิ **65°C – 75°C** ป้องกัน Throttling ได้ 100% เพิ่ม Throughput ได้ถึง ~90% โดยกินไฟเพิ่มเพียง ~10%

---

# ส่วนที่ 2: สถาปัตยกรรมคอมพิวเตอร์, ระบบบัส & การคำนวณหน่วยความจำ

*(อ้างอิง: บันทึกวิชา Computer Architecture and Buses)*

### 2.1 ระบบคอมพิวเตอร์ 3 ส่วน + 3 บัส
```
┌──────────────┐      ┌────────────┐      ┌──────────────┐
│  PROCESSOR   │      │   MEMORY   │      │  PERIPHERAL  │
│(CPU/ALU/Reg) │      │   ARRAY    │      │(GPIO/ADC/I2C)│
└──────┬───────┘      └─────┬──────┘      └──────┬───────┘
       │                    │                    │
═══════╪════════════════════╪════════════════════╪════  Address Bus (ทิศทางเดียว: CPU -> อุปกรณ์)
═══════╪════════════════════╪════════════════════╪════  Data Bus    (สองทิศทาง: อ่าน/เขียนข้อมูล)
═══════╪════════════════════╪════════════════════╪════  Control Bus (สัญญาณควบคุม: RD, WR, Clock)
```

* **Memory-Mapped I/O**: CPU มองอุปกรณ์รอบข้าง (Peripheral เช่น ADC, Timer, GPIO) เสมือนเป็นช่องหน่วยความจำช่องหนึ่งใน Address Map จึงใช้ชุดคำสั่งเดียวกันในการอ่านเขียน
* **วงจร Address Decoder & Chip Select (CS)**: ชิปแต่ละตัวจะมี Address Decoder คอยตรวจจับเลขที่อยู่บน Address Bus หากตรงกับช่วงของตัวเอง จะสร้างสัญญาณ **CS (Chip Select)** เพื่อเปิดการเชื่อมต่อกับ Data Bus

### 2.2 วงรอบ Fetch-Decode-Execute
1. **FETCH**: Control Unit ดึงค่าจาก Program Counter (PC) ส่งออก Address Bus + ส่งสัญญาณ Read (RD) ทาง Control Bus $\to$ Memory วางคำสั่ง (Opcode) ลง Data Bus $\to$ CPU รับคำสั่งเข้ามา
2. **DECODE**: Instruction Decoder ถอดรหัส Opcode ว่าต้องทำอะไร
3. **EXECUTE**: Control Unit สั่งการดึง Operand จาก Memory/Register ส่งให้ ALU คำนวณ แล้วเขียนผลลัพธ์กลับลง Register หรือ Memory จากนั้น $PC \leftarrow PC + 1$

### 2.3 สูตรการคำนวณขนาดหน่วยความจำและบัส
1. **ความจุหน่วยความจำสูงสุดที่ Address Bus เข้าถึงได้**:
   $$\mathbf{\text{Addressable Space} = 2^N \text{ Bytes}} \quad (N = \text{จำนวนบิตของ Address Bus})$$
   * $N=16 \implies 2^{16} = 65,536\text{ B} = \mathbf{64\text{ KB}}$
   * $N=24 \implies 2^{24} = 16,777,216\text{ B} = \mathbf{16\text{ MB}}$
   * $N=32 \implies 2^{32} = 4,294,967,296\text{ B} = \mathbf{4\text{ GB}}$
2. **Memory Bandwidth**:
   $$\mathbf{\text{Bandwidth (GB/s)} = \text{Bus Width (Bytes)} \times \text{Clock Frequency (GHz)} \times \text{DDR Factor}}$$
3. **พลังงานและระยะเวลาใช้งานแบตเตอรี่**:
   $$\mathbf{\text{Energy (Wh)} = \text{Capacity (Ah)} \times \text{Voltage (V)}}$$
   $$\mathbf{\text{Runtime (ชั่วโมง)} = \frac{\text{Energy (Wh)} \times \eta}{P_{\text{system}} \text{ (W)}}}$$
   *(โดย $\eta$ คือค่าประสิทธิภาพของวงจรแปลงไฟ ปกติ $0.80 - 0.90$)*

---

# ส่วนที่ 3: Deep Learning, CNN & การคำนวณโครงสร้างด้วยมือ

*(อ้างอิง: Lab 3 [Make Convolution], Lab 4 [CNN Architecture Calculation], ภาพถ่ายกระดาน และ Screenshot ใน Class)*

### 3.1 พื้นฐานโครงสร้าง Deep Learning และหน้าที่ของแต่ละ Layer (Deep Architecture Breakdown)

โครงข่ายประสาทเทียมเชิงลึก (Deep Neural Network: DNN) ประกอบด้วยโหนด (Artificial Neurons / Perceptrons) ที่เชื่อมโยงกันเป็นชั้นๆ (Layers) โดยข้อมูลจะไหลไปข้างหน้า (Feedforward) ผ่าน 3 องค์ประกอบหลัก:

```
[ Input Layer ] ──► [ Hidden Layer 1 ] ──► [ Hidden Layer 2 ] ──► ... ──► [ Output Layer ]
 (รับข้อมูลดิบ)        (สกัดฟีเจอร์ระดับต่ำ)     (สกัดฟีเจอร์ระดับสูง)           (ให้คำตอบ/ทำนาย)
```

---

#### 1. Input Layer (ชั้นรับข้อมูลนำเข้า)
* **บทบาทและหน้าที่**:
  * เป็นประตูด่านแรกในการรับข้อมูลดิบ (Raw Data) เข้าสู่โครงข่าย เช่น ค่าพิกเซลของภาพ (เช่น $28 \times 28 = 784$ จุด), สัญญาณเสียง, ค่าเซนเซอร์ IoT, หรือเวกเตอร์ของข้อความ
  * **ไม่มีการคำนวณทางคณิตศาสตร์ใดๆ (No Weights, No Biases)**: หน้าที่หลักมีเพียงการส่งผ่านค่าตัวเลข $x_1, x_2, \dots, x_n$ ต่อไปยัง Hidden Layer ถัดไป
  * ขนาดของ Input Layer จะถูกล็อกตายตัวตามมิติของข้อมูลนำเข้าเสมอ (Input Shape)

---

#### 2. Hidden Layer (ชั้นซ่อนเร้น - หัวใจของ Deep Learning)
* **ทำไมถึงเรียกว่า "Hidden Layer"?**: 
  * เพราะเป็นชั้นที่อยู่คั่นกลางระหว่าง Input และ Output ผู้ใช้งานภายนอกจะไม่เห็นค่าหรือปฏิสัมพันธ์โดยตรงในระหว่างการใช้งานปกติ
* **บทบาทและหน้าที่สำคัญ**:
  * **Feature Extraction & Transformation**: ทำหน้าที่แปลงข้อมูลจากมิติเดิมไปสู่มิติตัวแทนใหม่ (Representation Learning)
  * ชั้นที่อยู่ต้นๆ (Shallow Hidden Layers) จะตรวจจับฟีเจอร์ระดับพื้นฐาน (เช่น เส้นตรง, ขอบภาพ, จุดสี)
  * ชั้นที่อยู่ลึกถัดไป (Deeper Hidden Layers) จะรวมฟีเจอร์ง่ายๆ กลายเป็นรูปร่างซับซ้อน (เช่น ดวงตา, จมูก, ล้อรถ, จนถึงใบหน้าคนทั้งภาพ)
* **กลไกการคำนวณภายในแต่ละโหนดของ Hidden Layer**:
  1. **Linear Combination (Weighted Sum)**:
     $$z = \sum_{i=1}^{n} w_i x_i + b = \mathbf{W}^T \mathbf{x} + b$$
     โดยที่ $w_i$ คือ Weight (ค่าน้ำหนัก), $x_i$ คือ Input, และ $b$ คือ Bias (ค่าเอนเอียง)
  2. **Non-linear Activation Function**:
     $$a = g(z)$$
     * **ความสำคัญสูงสุดของ Activation Function ใน Hidden Layer**: หากไม่มีฟังก์ชันไม่เชิงเส้น ($g(z)$) ไม่ว่าจะต่อ Hidden Layer ทับซ้อนกันกี่สิบร้อยชั้น เครือข่ายทั้งหมดจะยุบตัวเทียบเท่ากับการแปลงเชิงเส้นชั้นเดียว ($W_2(W_1 x + b_1) + b_2 = W' x + b'$) ซึ่ง**ไม่สามารถแก้ปัญหาซับซ้อน (Non-linear Problems เช่น วงกลม หรือ XOR) ได้เลย**
* **Activation Functions ยอดนิยมใน Hidden Layer**:
  * **ReLU (Rectified Linear Unit)**: $f(x) = \max(0, x)$ — เป็นมาตรฐานหลักของโมเดลปัจจุบัน คำนวณเร็วมาก ป้องกันปัญหา Vanishing Gradient ในแดนบวก
  * **Leaky ReLU**: $f(x) = \max(\alpha x, x)$ โดย $\alpha \approx 0.01$ เพื่อแก้ปัญหา *Dying ReLU* (โหนดตายเมื่อค่าติดลบ)
  * **SiLU (Swish)**: $f(x) = x \cdot \sigma(x)$ — เรียบและให้ทางเดิน Gradient ลื่นไหล นิยมในโมเดลสมัยใหม่อย่าง YOLOv5
  * **Sigmoid / Tanh**: ยุคเก่าเคยใช้ใน Hidden Layer แต่ปัจจุบันเลี่ยงเนื่องจากเกิด Vanishing Gradient เมื่อเลเยอร์ลึกขึ้น
* **ข้อควรระวังเรื่องจำนวน Hidden Layers และ Nodes**:
  * *น้อยเกินไป (Under-capacity)*: เกิด **Underfitting** โมเดลไม่ฉลาดพอจะเรียนรู้ความสัมพันธ์
  * *มากเกินไป (Over-capacity)*: เกิด **Overfitting** โมเดลจำข้อมูลฝึกสอน กินแรม และประมวลผลช้าเกินกว่าจะรันบนบอร์ด Edge AI

---

#### 3. Output Layer (ชั้นแสดงผลลัพธ์)
* **บทบาทและหน้าที่**:
  * รับฟีเจอร์ระดับสูงสุดจาก Hidden Layer สุดท้าย มาสรุปคำตอบให้เป็นรูปแบบที่สอดคล้องกับโจทย์
* **จำนวนโหนดและ Activation ใน Output Layer ตามประเภทงาน**:
  | ประเภทงาน (Task) | จำนวนโหนดใน Output Layer | Activation Function ที่ใช้ | ฟังก์ชัน Loss ที่ใช้คู่กัน |
  | :--- | :---: | :---: | :---: |
  | **Binary Classification** (จำแนก 2 คลาส เช่น หมา vs แมว, มีหน้ากาก vs ไม่มี) | 1 โหนด (หรือ 2) | **Sigmoid** ($\sigma(z) \in [0, 1]$) | Binary Cross-Entropy (BCE) |
  | **Multi-class Classification** (เลือก 1 จาก $N$ คลาส เช่น ทายเลข 0–9) | $N$ โหนด | **Softmax** ($\sum P_i = 1$) | Categorical Cross-Entropy |
  | **Multi-label Classification** (1 รูปมีได้หลายคลาส เช่น มีทั้งหมวกและแว่น) | $N$ โหนด | **Sigmoid** รายโหนด | Binary Cross-Entropy รายโหนด |
  | **Regression** (ทำนายค่าต่อเนื่อง เช่น ทำนายราคา, พิกัด Bounding Box) | $M$ ค่าต่อเนื่อง | **Linear (None)** หรือ ReLU | MSE / MAE / Smooth L1 |

---

#### 4. ชนิดของ Specialized Layers ใน Deep Learning ยุคใหม่
นอกจาก Dense/Fully Connected Layer ทั่วไปแล้ว ในงาน Vision และ Edge AI ยังมีเลเยอร์สำคัญอื่นๆ ดังนี้:
1. **Convolutional Layer (Conv2D)**: ใช้ Kernel ขนาดเล็ก ($K \times K$) เลื่อนสแกนทั่วภาพ เพื่อดึงฟีเจอร์เชิงพื้นที่ (Spatial Features) โดยแชร์ค่าน้ำหนัก (Shared Weights) ช่วยประหยัดพารามิเตอร์
2. **Pooling / Subsampling Layer (MaxPool / AvgPool)**: ลดมิติ (Downsampling) ขนาดกว้าง$\times$ยาวของ Feature Map ทำให้โมเดลทนต่อการขยับย้ายตำแหน่ง (Translation Invariance) และลดภาระการคำนวณ **ไม่มีพารามิเตอร์ที่ต้องเทรน (0 Params)**
3. **Batch Normalization (BatchNorm) Layer**: ปรับสเกลค่า Feature Map ให้มี Mean ใกล้ 0 และ Variance ใกล้ 1 ช่วยให้เทรนโมเดลได้เร็วขึ้น ไม่ติดหล่ม Gradient และทำหน้าที่เป็น Regularizer ทางอ้อม
4. **Dropout Layer**: สุ่มปิดการทำงานของโหนดใน Hidden Layer บางส่วนชั่วคราวขณะเทรน (เช่น $p = 0.2-0.5$) เพื่อป้องกันไม่ให้โหนดพึ่งพากันมากเกินไป แก้ปัญหา **Overfitting** (ถูกปิดการทำงานในโหมด Inference/Test)
5. **Flatten Layer**: ยุบข้อมูลมิติหลายแกน (เช่น ภาพ 3D: $C \times H \times W$) ให้กลายเป็นเวกเตอร์ 1D แบนราบ เพื่อป้อนเข้า Fully Connected Layer ต่อไป

---

### 3.2 จุดเด่น 3 ประการของ CNN
1. **Local Receptive Fields**: สนใจความสัมพันธ์ของพิกเซลที่อยู่ใกล้เคียงกันเพื่อดึงลักษณะเด่น
2. **Shared Weights**: ใช้ฟิลเตอร์ค่าน้ำหนักชุดเดียวกันสแกนทั่วทั้งภาพ ช่วยลดพารามิเตอร์ลงอย่างมหาศาล
3. **Subsampling / Pooling**: ย่อขนาดมิติข้อมูล ช่วยให้ทนทานต่อการบิดเบี้ยว/การขยับเลื่อนตำแหน่ง และป้องกัน Overfitting

---

### 3.3 สูตรมาตรฐานการคำนวณมิติ Output (หัวใจข้อสอบ)

$$\mathbf{\text{Output Size} = \left\lfloor \frac{W - K + 2P}{S} \right\rfloor + 1}$$

* $W$ = ขนาด Input (Width/Height)
* $K$ = ขนาด Kernel / Filter / Pooling window
* $P$ = ขนาด Padding (การเติมขอบ 0)
* $S$ = Stride (ระยะก้าวเดินทีละกี่ช่อง)
* $+1$ = ต้องบวก 1 เสมอ เพราะรวมตำแหน่งตั้งต้นตำแหน่งแรก

> ❓ **คำถามยอดฮิต: ทำไมใน Pooling ถึงเขียนเป็น $\frac{60 - 2}{2} + 1$?**  
> **ตอบ**: เลข **$-2$ มาจาก $-K$** นั่นเอง! เพราะ Pooling มีขนาดกรอบ $2 \times 2$ ($K=2$) และไม่มี Padding ($P=0$) เมื่อแทนในสูตร $\frac{W - K + 2P}{S} + 1$ จึงได้ $\frac{60 - 2 + 0}{2} + 1 = \mathbf{30}$  
> *(หรือคิดลัดเมื่อ $K=S$: $\frac{W}{K} = \frac{60}{2} = \mathbf{30}$)*

---

### 3.4 สูตรคำนวณจำนวน Parameters
* **Convolution Layer**:
  $$\mathbf{\text{Params} = (K_w \times K_h \times C_{\text{in}} + 1) \times C_{\text{out}}}$$
  *(หมายเหตุ: $+1$ คือ Bias ต่อ 1 ฟิลเตอร์)*
* **Fully Connected Layer**:
  $$\mathbf{\text{Params} = (N_{\text{in}} + 1) \times N_{\text{out}}}$$
* **Pooling Layer**: **ไม่มีพารามิเตอร์สำหรับการเทรน (0 Params)**

---

### 3.5 ตัวอย่างคำนวณด้วยมือจริง (โจทย์งานในชั้นเรียน)

#### ข้อที่ 1: การคำนวณ Convolution $6 \times 6$ ด้วย Kernel $3 \times 3$ (จากใบงาน Week 3)

**Input ($6 \times 6$) และ Kernel ($3 \times 3$)**:

$$\text{Input} = \begin{bmatrix} 1 & 1 & 1 & 0 & 0 & 1 \\ 0 & 1 & 1 & 0 & 1 & 1 \\ 0 & 0 & 1 & 0 & 0 & 1 \\ 0 & 0 & 1 & 1 & 1 & 0 \\ 1 & 0 & 1 & 1 & 1 & 1 \\ 0 & 0 & 1 & 0 & 1 & 1 \end{bmatrix}, \quad \text{Kernel } K = \begin{bmatrix} 0 & 0 & 1 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{bmatrix}$$

**ขนาดของ Output Feature Map**:

$$W_{\text{out}} = \frac{6 - 3 + 0}{1} + 1 = \mathbf{4 \times 4}$$

**ผลลัพธ์ Feature Map ($4 \times 4$)**:

$$\text{Feature Map} = \begin{bmatrix} 4 & 1 & 1 & 4 \\ 3 & 2 & 2 & 2 \\ 3 & 3 & 3 & 3 \\ 3 & 3 & 4 & 3 \end{bmatrix}$$

**การทำ Max Pooling ($2 \times 2, \text{Stride}=2$)**:
* บล็อกบนซ้าย: $\max(4, 1, 3, 2) = \mathbf{4}$
* บล็อกบนขวา: $\max(1, 4, 2, 2) = \mathbf{4}$
* บล็อกล่างซ้าย: $\max(3, 3, 3, 3) = \mathbf{3}$
* บล็อกล่างขวา: $\max(3, 3, 4, 3) = \mathbf{4}$

**ผลลัพธ์สุดท้าย ($2 \times 2$)**:

$$\text{Pooled Output} = \begin{bmatrix} 4 & 4 \\ 3 & 4 \end{bmatrix}$$

---

#### ข้อที่ 2: โครงสร้าง LeNet Pipeline คำนวณทีละชั้น (จาก Lab 4)
* **Input**: ภาพ Grayscale ขนาด $32 \times 32$ ($C_{\text{in}} = 1$)
1. **$C_1$ (Conv)**: Filter $5 \times 5, P=0, S=1, 3\text{ Maps} \implies \frac{32 - 5 + 0}{1} + 1 = \mathbf{28 \times 28}$ (สกัดฟีเจอร์ระดับต่ำ)
2. **$S_2$ (Max Pool)**: Pool $2 \times 2, S=2 \implies \frac{28}{2} = \mathbf{14 \times 14}$ (ย่อขนาดภาพ สกัดฟีเจอร์เด่น)
3. **$C_3$ (Conv)**: Filter $5 \times 5, P=0, S=1, 6\text{ Maps} \implies \frac{14 - 5 + 0}{1} + 1 = \mathbf{10 \times 10}$ (สกัดฟีเจอร์ซับซ้อน)
4. **$S_4$ (Max Pool)**: Pool $2 \times 2, S=2 \implies \frac{10}{2} = \mathbf{5 \times 5}$
5. **$C_5$ (Conv)**: Filter $5 \times 5, P=0, S=1, 48\text{ Maps} \implies \frac{5 - 5 + 0}{1} + 1 = \mathbf{1 \times 1}$ (ได้ 48 โหนด ขนาด $1 \times 1$)
6. **$F_6$ (Fully Connected)**: กำหนด Hyperparameter มี **32 Nodes**
   * *เกณฑ์การเลือกจำนวนโหนด*:
     * น้อยเกินไป: คำนวณไว แต่โมเดลไม่เก่ง เกิด **Underfitting**
     * มากเกินไป: โมเดลช้า กินแรม และจำข้อสอบ เกิด **Overfitting**
7. **Output Layer**: **10 Nodes** (จำแนกตัวเลข 0–9 ผ่าน Softmax)

---

#### ข้อที่ 3: การคำนวณ Forward Propagation ของ MLP (จากภาพ Screenshot ใน Class)
* **Input**: $x_1 = 1.5, \quad x_2 = -2.0, \quad x_3 = 0.5$, มีค่า Bias ขาเข้า $b_{\text{in}} = 1.0$
* **Weights (Input $\to$ Hidden)**:
  * Node 1: $w_{11} = 0.4, \quad w_{12} = -0.3, \quad w_{13} = 0.7, \quad b_1 = 0.8$
  * Node 2: $w_{21} = -0.6, \quad w_{22} = 0.5, \quad w_{23} = -0.2, \quad b_2 = -0.4$
* **คำนวณ Hidden Node 1 ($z_1$)**:
  $$z_1 = (0.4 \times 1.5) + (-0.3 \times -2.0) + (0.7 \times 0.5) + (0.8 \times 1.0) = 0.6 + 0.6 + 0.35 + 0.8 = \mathbf{2.35}$$
* **คำนวณ Hidden Node 2 ($z_2$)**:
  $$z_2 = (-0.6 \times 1.5) + (0.5 \times -2.0) + (-0.2 \times 0.5) + (-0.4 \times 1.0) = -0.9 - 1.0 - 0.1 - 0.4 = \mathbf{-2.40}$$
* **Weights (Hidden $\to$ Output)**:
  * Bias ชั้น Hidden $b_{\text{hid}} = 1.0$
  * น้ำหนักเชื่อมโยง: $w_{\text{out}, 1} = 1.2, \quad w_{\text{out}, 2} = -0.7, \quad b_{\text{out}} = 0.5$
* **คำนวณ Output Node ($z_{\text{out}}$)**:
  $$z_{\text{out}} = (1.2 \times 2.35) + (-0.7 \times -2.40) + (0.5 \times 1.0) = 2.82 + 1.68 + 0.5 = \mathbf{5.00}$$

---

# ส่วนที่ 4: กลไก 5 เลเยอร์หลักของ LLM และการปรับใช้บน Edge

*(อ้างอิง: ภาพถ่ายใบงาน Week 2 "อธิบายการทำงานของ LLM" วันที่ 13 ก.ค. 2026)*

```
Input Text ──► [1. Tokenization] ──► [2. Embedding] ──► [3. Transformer (Self-Attention + FFN)]
                                                                         │
Output Text ◄── [5. Detokenization] ◄── [4. Linear & Softmax] ◄──────────┘
      │
      └──── Loop ย้อนกลับไปทำนาย Token ถัดไปจนกว่าจะพบคำสั่งหยุด (EOS Token) ────┘
```

1. **Layer 1: Tokenization**:
   * แปลงข้อมูลข้อความดิบ (Raw text) แบ่งออกเป็นชิ้นเล็กๆ เรียกว่า **Token**
   * แปลง Token แต่ละตัวให้อยู่ในรูปตัวเลขรหัสประจำตัว (**Token ID**) ตาม Vocabulary ของโมเดล
2. **Layer 2: Embedding**:
   * นำ Token ID มาแมปเข้าสู่เวกเตอร์เชิงลึกหลายมิติ (**Word Vector**)
   * รวมค่า **Positional Encoding** เข้ากับเวกเตอร์ เพื่อระบุตำแหน่งลำดับคำในประโยค
3. **Layer 3: Transformer Block**:
   * **Self-Attention**: นำเวกเตอร์แต่ละคำมาคำนวณ weight เพื่อหาความสัมพันธ์เชื่อมโยงระหว่างคำแต่ละคำในประโยค
   * **Feed-Forward Network (FFN)**: นำเวกเตอร์จาก Self-Attention ส่งไปสกัดฟีเจอร์ความหมายเชิงลึกต่อ
4. **Layer 4: Linear & Softmax**:
   * นำเวกเตอร์ที่เข้าใจความหมายประโยคอย่างสมบูรณ์ มาขยายออกผ่านสมการ Linear ให้เท่ากับจำนวนคำทั้งหมดในโมเดล (**Vocab Size**) ได้คะแนนดิบ (**Logits**)
   * ผ่าน **Softmax** แปลงค่า Logits เป็นความน่าจะเป็น เพื่อให้โมเดลเลือกคำตอบที่เหมาะสมที่สุดทีละคำ
5. **Layer 5: Detokenization**:
   * แปลง Token ID ที่ระบบเลือกได้กลับมาเป็นข้อความ (Text)
   * ระบบจะนำคำที่ได้ใหม่นี้กลับไปวนลูป (Autoregressive Loop) ส่งเป็นอินพุตต่อท้ายประโยคเดิมไปเรื่อยๆ จนกระทั่งเจอคำสั่งหยุด (**EOS: End of Sequence Token**) จึงจบ session ของคำตอบ

### การปรับใช้ LLM บน Edge (Model Quantization)
* **ปัญหา**: โมเดลระดับ 7B พารามิเตอร์ ที่ FP16 ต้องใช้ RAM ถึง $14\text{ GB}$ และติดคอขวดแบนด์วิดท์แรม
* **วิธีแก้**: ทำ **Quantization (INT8 หรือ INT4)** ลดขนาดโมเดลเหลือเพียง **~4–5 GB** ทำให้รันบนบอร์ด Edge ได้ (เช่น Llama.cpp, Ollama)

---

# ส่วนที่ 5: เจาะลึกผังโครงสร้างสถาปัตยกรรม YOLOv4 vs YOLOv5

*(อ้างอิง: ภาพถ่ายบันทึกการสอนเปรียบเทียบในชั้นเรียน Week 6 วันที่ 17 ส.ค. 2026 อย่างละเอียดทุกจุด)*

```
       [สถาปัตยกรรม YOLOv4]                                  [สถาปัตยกรรม YOLOv5]
   Input Tensor (3, 640, 640)                            Input Tensor (3, 640, 640)
               │                                                     │
  Conv2D (3x3, S=1) + BN + Mish                         Slice -> Interleave 2x2 (4 patch)
   (สกัด feature, BN=norm, Mish=ReLU)                         (12, 320, 320) ตัดรูปไม่เสียพิกเซล
               │                                                     │
  Conv2D (3x3, S=2) + BN + Mish                         Conv2D (3x3, S=1) + BN + SiLU
   (ลดขนาดภาพ, เพิ่มมิติ feature)                            (64, 320, 320, SiLU เรียบ เก็บ grad ดี)
         (64, 320, 320)                                              │
               │                                              [C3 Block (CSP)]
         [CSP Block]                                   Conv1x1 (Base) ──┬── Conv1x1 (Bypass)
  Conv1x1 (Base) ──┬── Conv1x1 (Bypass)                      │          │
        │          │   (รักษา feature ไว้)             Bottleneck x N   │
   ResUnit x N     │                                         └───┬──────┘
        │          │                                           Concat -> Conv1x1
     Conv1x1       │                                                 │
        └───┬──────┘                                              [SPPF]
     Concat (C/2 + C/2 = C)                              Bypass X0 ──┬── MaxPool 5x1
            │                                                        │   (รอบ 1 ขนาด 5)
         Conv1x1                                                     ├── MaxPool 5x2 (เทียบเท่า 9)
            │                                                        │   (รอบ 2 ขนาด 9)
          [SPP]                                                      └── MaxPool 5x3 (เทียบเท่า 13)
  Bypass X0 ──┬── MaxPool 5 (กรอบเล็ก)                               │   (รอบ 3 ขนาด 13)
              ├── MaxPool 9 (กรอบกลาง)                         Concat x4 -> Conv1x1
              └── MaxPool 13 (กรอบใหญ่)                              │   (อนุกรม เร็วกว่า SPP เท่าตัว)
              │                                                [Neck: C3 + Bottleneck]
         Concat x4 -> Conv1x1                                        │
            │                                                        ▼
         [Neck: PANet]                                   Feature Pyramid Map (ทั้งสอง)
  Top-Down+UpSample & Lateral (ตื้น)                     • P3 (S=8):  80x80x3 (วัตถุเล็ก)
  Concat -> Conv1x1 -> Conv3x3 -> Conv1x1                • P4 (S=16): 40x40x3 (วัตถุกลาง)
                                                         • P5 (S=32): 20x20x3 (วัตถุใหญ่)
                                                         รวม = 25,200 กล่อง / ภาพ
```

---

### 5.1 รายละเอียดการทำงานของแต่ละส่วน (แกะจากบันทึกใน Class)

#### 1. Input Processing:
* **YOLOv4**: ใช้ **Conv2D ($3\times3, S=1$)** ตามด้วย **Conv2D ($3\times3, S=2$)** เพื่อลดขนาดรูปและเพิ่มมิติ Feature Map
* **YOLOv5**: ใช้ **Slice Layer $\to$ Interleave $2\times2$ (4 patch)**
  * ตัดรูปขนาด $(3, 640, 640)$ ออกเป็น 4 ชิ้นย่อยแล้วประกบแชนแนล กลายเป็น $(12, 320, 320)$
  * **จุดเด่น**: *เก็บรายละเอียดข้อมูลภาพได้ครบถ้วนกว่า v4 โดยไม่สูญเสียข้อมูลพิกเซลไปจากการตัดลด*

#### 2. Activation Function:
* **YOLOv4**: ใช้ **Mish** ($Mish = x \cdot \tanh(\ln(1+e^x))$) คล้าย ReLU แต่มีความหน่วงในการคำนวณสูงกว่า
* **YOLOv5**: ใช้ **SiLU (Swish)** ($SiLU = x \cdot \sigma(x)$)
  * **จุดเด่น**: เส้นกราฟเรียบ กักเก็บ Gradient ช่วยให้สัญญาณ Gradient ไหลย้อนกลับ (Backpropagation) ได้ดีกว่า ReLU และประมวลผลเร็วกว่า Mish

#### 3. Backbone Structure (CSP vs C3):
* **YOLOv4 (CSP + ResUnit)**:
  * แบ่ง Channel ออกเป็น 2 สาย ($C/2$):
    * สายที่ 1 (Base): ผ่าน `Conv 1x1` (ลดมิติ) $\to$ `ResUnit x N` (สกัด feature loop) $\to$ `Conv 1x1` (รวม feature ใน loop)
    * สายที่ 2 (Bypass): ผ่าน `Conv 1x1` เพื่อรักษา feature ดั้งเดิมไว้ แล้วนำมารวมกันปลายทางก่อน Concat
    * ทำ `Concat` $[B, (C/2)_{\text{main}} + (C/2)_{\text{bypass}}, H, W] \implies C/2 + C/2 = C$
    * ปิดท้ายด้วย `Conv 1x1` เพื่อรวมเลเยอร์จากหลาย Channel ให้เป็นเนื้อเดียวกัน
* **YOLOv5 (C3 Block)**:
  * ย่อมาจาก **Cross-Stage Partial with 3 Convolutions**
  * สายที่ 1 ผ่าน `Conv 1x1` $\to$ **`Bottleneck x N`** (โดย 1 Bottleneck ประกอบด้วย $[\text{Conv } 1\times1 \to \text{Conv } 3\times3]$)
  * ค่า $N$ ยืดหยุ่นปรับได้ตามขนาดโมเดล: **`-n` (Nano), `-s` (Small), `-m` (Medium), `-l` (Large), `-x` (Extra Large)**
  * สูตรสมการของ C3 ตามบันทึก:
    $$\mathbf{Y = \text{Conv}_3\left( [ B_N(\text{Conv}_1(x)) \parallel \text{Conv}_2(x) ] \right)}$$
    *(โดย $\parallel$ คือ Concatenate, $\text{Conv} = 1\times1 (BN + SiLU)$, และ $B_N$ คือการวน Loop $N$ บล็อก)*

#### 4. Spatial Pooling (SPP vs SPPF):
* **YOLOv4 (SPP - ขนาน)**:
  * ทำ MaxPool 3 ขนาดขนานกัน:
    * $x_1$: `MaxPool 5` (กรอง feature เด่นในกรอบเล็ก)
    * $x_2$: `MaxPool 9` (กรอบกลาง)
    * $x_3$: `MaxPool 13` (กรอบใหญ่)
    * รวมกับสาย Bypass $X_0$ แล้วทำ `Concat x4` $\to$ `Conv 1x1`
* **YOLOv5 (SPPF - Spatial Pyramid Pooling Fast อนุกรม)**:
  * แทนที่จะคำนวณขนานกัน v5 ใช้ **MaxPool ขนาด $5\times5$ ตัวเดียว ต่ออนุกรมกัน 3 ครั้ง**:
    * รอบที่ 1: `MaxPool 5 x 1` (ขนาดเทียบเท่า 5)
    * รอบที่ 2: `MaxPool 5 x 2` $\implies 5 + (5 - 1) = \mathbf{9}$ (ขนาดเทียบเท่า 9)
    * รอบที่ 3: `MaxPool 5 x 3` $\implies 9 + (5 - 1) = \mathbf{13}$ (ขนาดเทียบเท่า 13)
  * **จุดเด่น**: *ผลลัพธ์ทางคณิตศาสตร์ออกมาเหมือนกับ SPP ของ v4 ทุกประการ แต่การคิดแบบอนุกรมทำให้ความเร็วในการคำนวณสูงกว่าเกือบ 2 เท่า!*

#### 5. Feature Pyramid Map & Output Vector:
* **Feature Pyramid Map 3 ระดับสเกล**:
  * **$P_3$** (Stride $S=8$): ขนาด $80 \times 80 \times 3$ $\implies$ ความละเอียดสูง สำหรับ**วัตถุขนาดเล็ก**
  * **$P_4$** (Stride $S=16$): ขนาด $40 \times 40 \times 3$ $\implies$ ความละเอียดปานกลาง สำหรับ**วัตถุขนาดกลาง**
  * **$P_5$** (Stride $S=32$): ขนาด $20 \times 20 \times 3$ $\implies$ ความละเอียดต่ำ สำหรับ**วัตถุขนาดใหญ่**
* **การคำนวณจำนวน Bounding Boxes รวม**:
  $$\text{Total Boxes} = (80^2 + 40^2 + 20^2) \times 3 = (6,400 + 1,600 + 400) \times 3 = 8,400 \times 3 = \mathbf{25,200\text{ กล่อง / ภาพ}}$$
* **รูปแบบ Output Vector ต่อ 1 กล่อง (เก็บค่า $5 + C$ ค่า)**:
  $$\mathbf{[t_x, t_y, t_w, t_h, P_{\text{obj}}, c_1, c_2, \dots, c_n]}$$
  * $[t_x, t_y, t_w, t_h]$: พิกัดตำแหน่งและขนาดของกล่อง
  * $P_{\text{obj}}$: ความน่าจะเป็นว่ามีวัตถุอยู่ในกล่อง (Objectness Score)
  * $c_1, c_2, \dots, c_n$: ประเภทของวัตถุและความน่าจะเป็นในแต่ละ Class

---

### 5.2 ตารางสรุปเปรียบเทียบ YOLOv4 vs YOLOv5 (ตามกรอบสรุปในกระดาษ)

| หัวข้อ | YOLOv4 | YOLOv5 | ความหมายเชิงวิศวกรรม |
|---|---|---|---|
| **Input** | Conv $3\times3$ ลดรูป | **Slice รูป (Focus)** | v5 ไม่เสีย Pixel เก็บรายละเอียดภาพได้ครบถ้วนกว่า |
| **Activation** | Mish (หนัก) | **SiLU (Swish)** | v5 เบากว่า คำนวณง่ายกว่า ไวกว่า และ Gradient ไหลดี |
| **Backbone** | ซับซ้อน (CSP + ResUnit) | **อนุกรม (C3 Bottleneck)** | v5 โครงสร้าง C3 ปรับขนาด $N$ ได้ยืดหยุ่น ($n, s, m, l, x$) |
| **Pooling** | ขนาน (SPP) | **อนุกรมเร็วกว่า (SPPF)** | v5 ทำ MaxPool $5\times5$ ต่ออนุกรม ได้ผลเท่าเดิมแต่ไวกว่าเท่าตัว |
| **Model** | ค่อนข้างตายตัว | **ปรับได้หลากหลาย** | v5 มีตั้งแต่ Nano (รันบน Edge ได้) จนถึง XLarge |

---

# ส่วนที่ 6: กรณีศึกษาระบบตรวจจับ PPE บน Raspberry Pi 4 และโมเดล Edge อื่นๆ

*(อ้างอิง: รายงาน PPE และรายงาน ML, DL, RL on Edge)*

### 6.1 ทำไมเลือก SSD MobileNet v2 แทน YOLO บน Raspberry Pi 4?
* จากการทดสอบวัดค่าจริงบน Raspberry Pi 4 (BCM2711 CPU Standalone):
  * **SSD MobileNet v2**: ได้ **16.24 FPS** (Latency 58.02 ms)
  * **YOLOv8n / YOLOv26n**: ได้เพียง **2.39 FPS** (Latency 418.4 ms) $\implies$ **ช้ากว่าประมาณ 7 เท่า!**
  * เหตุผล: SSD MobileNet มีสถาปัตยกรรม Depthwise Separable Convolution ที่เบามาก เหมาะกับ CPU ของ RPi 4 จึงไม่ทำให้เกิดความร้อนสะสมจน CPU Throttling
* **การเสริมด้วย Google Coral Edge TPU**:
  * ช่วยลด Latency ของ SSD MobileNet ลงเหลือเพียง **20.37 ms (~18.14 FPS)**
  * ข้อควรระวัง: โมเดลตระกูล YOLO บางรุ่นเมื่อนำมารันบน Coral กลับช้าลง (567 ms) เนื่องจากโครงสร้าง Layer บางตัวไม่รองรับบน EdgeTPU ต้องเสียเวลาสลับกลับไปรันบน CPU

### 6.2 โมเดล Sequence & Reinforcement Learning บน Edge
1. **RNN**: ข้อมูลวนซ้ำตามเวลา จุดอ่อนคือ **Vanishing Gradient** (ลืมอดีต) บน Edge นิยมแปลงเป็นโค้ดภาษา C ตรงๆ ใช้ INT8 บน MCU สำหรับงานตรวจจับความผิดปกติจากการสั่นสะเทือน (Vibration Anomaly)
2. **LSTM**: แก้ปัญหาด้วย **Cell State ($C_t$)** เป็นทางด่วนความจำ ควบคุมด้วย 3 Gate (*Forget, Input, Output*)
3. **GRU**: รวม Cell State กับ Hidden State เข้าด้วยกัน และลดเหลือเพียง 2 Gate (*Update, Reset*) **ลดพารามิเตอร์ลงราว 25%** เมื่อเทียบกับ LSTM เหมาะสำหรับงาน Edge ที่มี RAM จำกัด
4. **Q-Learning vs DQN**:
   * *Q-Learning (Tabular)*: ต้องสร้างตาราง $Q(s, a)$ เมื่อ State เป็นภาพต่อเนื่อง จะเกิดปัญหาตารางระเบิด (Curse of Dimensionality) จน RAM บอร์ดไม่พอ
   * *DQN (Deep Q-Network)*: ใช้ Neural Network (เช่น CNN) เข้ามาประมาณค่าฟังก์ชัน $Q$ แทนตาราง มี **Replay Buffer** ป้องกัน Correlation และ **Target Network** ช่วยให้การฝึกมีความเสถียร

---

# ส่วนที่ 7: การวิเคราะห์และเปรียบเทียบบอร์ด Edge AI ทั้ง 8 ตัว

*(อ้างอิง: ตารางเปรียบเทียบสเปกฮาร์ดแวร์ และเกณฑ์การรองรับภาระงาน)*

```
[พลังประมวลผล AI สูงมาก: 200 - 2,000+ TOPS] ──► Thor, IGX Orin, Jetson AGX Orin (ยานยนต์, ผ่าตัด, AMR)
[พลังประมวลผล AI ปานกลาง: 6 - 15 TOPS]      ──► RB3 Gen 2, Orange Pi 5 (โดรน, เกตเวย์, สมาร์ทโฮม)
[พลังประมวลผล AI ระดับเริ่มต้น/จอภาพ: 3.2 TOPS]──► Khadas VIM4 (ป้ายโฆษณา, Kiosk, Smart Screen)
[ไม่มี NPU ในตัว: 0 TOPS]                   ──► Raspberry Pi 5 (การศึกษา, Maker, Server จิ๋ว)
[Ultra-Low Power ไมโครคอนโทรลเลอร์: < 2W]   ──► STM32N6 (TinyML, เช็คการสั่นสะเทือนมอเตอร์)
```

### 7.1 รายละเอียดสเปกและการใช้งานจริงทั้ง 8 บอร์ด

#### 1. NVIDIA IGX Thor
* **สเปก**: SoC Thor, 14-core Neoverse V3AE, GPU Blackwell, **~1,000 – 2,000+ TOPS (FP8/INT8)**, RAM สูงสุด 128GB LPDDR5X (>500 GB/s), ไฟ 200W – 500W+
* **เหมาะกับงาน**: **งานระดับความปลอดภัยสูงสุด (Safety-Critical)** เช่น หุ่นยนต์ผ่าตัดทางการแพทย์ (Surgical Robotics), ยานยนต์ขับเคลื่อนอัตโนมัติขั้นสูง (ASIL-D / IEC 61508)
* **จุดเด่น**: พลังระดับซูเปอร์คอมพิวเตอร์ที่ Edge รองรับ Foundation Models และ Generative AI หลายโมเดลพร้อมกันแบบ Zero-latency

#### 2. NVIDIA IGX Orin
* **สเปก**: Orin Industrial SoC, 12-core A78AE, GPU Ampere (2048 CUDA, 64 Tensor), **275 TOPS** (บอร์ดเดี่ยว) / **700 – 1,700+ TOPS** (เมื่อต่อ dGPU), RAM 64GB LPDDR5 ECC (204.8 GB/s), ไฟ 150W – 250W
* **เหมาะกับงาน**: **เครื่องมือแพทย์วินิจฉัยภาพขั้นสูง (Medical Imaging)** เช่น เครื่อง Ultrasound/CT/MRI Real-time, เวิร์กสเตชันควบคุมความปลอดภัยในโรงงานอุตสาหกรรม

#### 3. NVIDIA Jetson AGX Orin
* **สเปก**: 12-core Cortex-A78AE @ 2.2 GHz, GPU Ampere (2048 CUDA, 64 Tensor) + 2x NVDLA 2.0, **200 – 275 TOPS**, RAM 32GB/64GB LPDDR5 (204.8 GB/s), ไฟ **15W – 60W**
* **เหมาะกับงาน**: ⭐ **หุ่นยนต์เคลื่อนที่อัตโนมัติ (AMR), แขนกลหุ่นยนต์, หุ่นยนต์ฮิวแมนนอยด์ (Humanoid Robot)** และระบบกล้อง Edge Multi-Camera
* **ทำไมจึงสมดุลที่สุด**: ให้พลัง AI มหาศาลถึง 275 TOPS แต่กินไฟเพียง 15W–60W สามารถใช้แบตเตอรี่ขับเคลื่อนได้ยาวนาน และมี 2x NVDLA ช่วยแบ่งเบาภาระงาน Vision ได้อย่างอิสระ

#### 4. Orange Pi 5 / 5 Plus
* **สเปก**: Rockchip RK3588, 8-core (4x A76 + 4x A55), GPU Mali-G610 MP4, **6 TOPS (Tri-core NPU)**, RAM 4GB – 32GB LPDDR4/4x (~34 GB/s), ไฟ 5W – 15W
* **เหมาะกับงาน**: **Smart Home Hub, Edge Gateway ต้นทุนต่ำ, Basic Object Detection**
* **จุดเด่น**: ความคุ้มค่าด้านงบประมาณ มี NPU 6 TOPS เพียงพอสำหรับรันโมเดล YOLOv5s/YOLOv8n ขนาดเล็ก 1–2 สตรีมแบบเรียลไทม์

#### 5. Qualcomm RB3 Gen 2
* **สเปก**: Qualcomm QCS6490, 8-core Kryo 670, GPU Adreno 643, **~12 – 15 TOPS (Hexagon NPU + AI Engine)**, RAM 8GB/16GB, ไฟ 5W – 15W
* **เหมาะกับงาน**: **โดรนเชิงพาณิชย์ (Commercial Drones), หุ่นยนต์บริการ (Service Robots), กล้องตรวจการณ์อัจฉริยะ**
* **จุดเด่น**: ออกแบบมาสำหรับอุปกรณ์พกพาไร้สาย กินไฟต่ำ รองรับ Wi-Fi 6E และ 5G ในตัว ประมวลผลภาพจากกล้องหลายตัวพร้อมกัน

#### 6. Raspberry Pi 5
* **สเปก**: Broadcom BCM2712, 4-core Cortex-A76 @ 2.4 GHz, GPU VideoCore VII, **0 TOPS (ไม่มี NPU ในตัว)**, RAM 2GB – 16GB LPDDR4X (17 GB/s), ไฟ 5W – 12W
* **เหมาะกับงาน**: **การศึกษา, โค้ดดิ้ง, โปรเจกต์ Maker, Server จิ๋วในบ้าน, IoT Gateway เก็บรวบรวมข้อมูลเซนเซอร์**
* **ข้อจำกัด**: ไม่มี NPU หากจะรันโมเดล AI ต้องคำนวณผ่าน CPU หรือซื้อการ์ดเสริม เช่น Raspberry Pi AI HAT+ (ชิป Hailo 13/26 TOPS)

#### 7. Khadas VIM4
* **สเปก**: Amlogic A311D2, 8-core (4x A73 + 4x A53), GPU Mali-G52 MP8, **3.2 TOPS (Amlogic NPU)**, RAM 8GB LPDDR4X, ไฟ 5W – 12W
* **เหมาะกับงาน**: **Smart Display, ป้ายโฆษณาดิจิทัลอัจฉริยะ (Digital Signage), ตู้ Kiosk อัตโนมัติ, ระบบประชุมวิดีโอ**
* **จุดเด่น**: เด่นด้านการประมวลผลภาพออกหน้าจอระดับ 4K มี NPU ขนาดเล็กสำหรับตรวจจับใบหน้าหรือตรวจวัดความสนใจของผู้ชมหน้าจอ

#### 8. STM32N6 (STM32N657)
* **สเปก**: ไมโครคอนโทรลเลอร์ (MCU) ARM Cortex-M55 @ 800 MHz (Helium), **~0.6 – 3 TOPS (Neural-ART NPU)**, RAM 4.2 MB On-chip SRAM, ไฟ **< 1W – 2W**
* **เหมาะกับงาน**: **TinyML, เซนเซอร์ตรวจจับความผิดปกติของมอเตอร์ (Predictive Maintenance), ตรวจจับเสียงเฉพาะคำ (Keyword Spotting)**
* **จุดเด่น**: เป็นระดับ MCU กินไฟต่ำกว่า 2 วัตต์ เปิดเครื่องพร้อมทำงานทันที (Instant On) ทำงานบนแบตเตอรี่ก้อนเล็กได้ยาวนานหลายเดือนถึงเป็นปี

---

### 7.2 ตารางสรุปคุณสมบัติเปรียบเทียบบอร์ดทั้ง 8 ตัว

| ลำดับ | ชื่อบอร์ด | ชิปประมวลผล (SoC) | สถาปัตยกรรม CPU | หน่วยประมวลผล AI | RAM & แบนด์วิดท์ | กำลังไฟ (TDP) | กลุ่มการใช้งานหลัก |
|:---:|---|---|---|:---:|:---:|:---:|---|
| **1** | **NVIDIA IGX Thor** | NVIDIA Thor | ARM Neoverse V3AE (14 คอร์) | **~1,000 – 2,000+ TOPS** | สูงสุด 128GB LPDDR5X (>500 GB/s) | 200W – 500W+ | Industrial/Medical AI, Surgical Robotics, ASIL-D |
| **2** | **NVIDIA IGX Orin** | Orin Industrial | 12-core ARM Cortex-A78AE | **275 TOPS** (บอร์ดเดี่ยว)<br>**700 – 1,700+ TOPS** (dGPU) | 64GB LPDDR5 ECC (204.8 GB/s) | 150W – 250W | Medical Imaging, Industrial Workstation, Factory Safety |
| **3** | **NVIDIA Jetson AGX Orin** | Jetson AGX Orin | 12-core ARM Cortex-A78AE | **200 – 275 TOPS** | 32GB / 64GB LPDDR5 (204.8 GB/s) | **15W – 60W** | Autonomous Mobile Robots (AMR), Multi-Camera Edge Vision |
| **4** | **Orange Pi 5 / 5 Plus** | Rockchip RK3588 | 8-core (4x A76 + 4x A55) | **6 TOPS** (Tri-core NPU) | 4GB – 32GB LPDDR4/4x (~34 GB/s) | 5W – 15W | Smart Home, Edge Gateway, Basic Object Detection |
| **5** | **Qualcomm RB3 Gen 2** | Qualcomm QCS6490 | 8-core Qualcomm Kryo 670 | **~12 – 15 TOPS** | 8GB / 16GB LPDDR4x/5 | 5W – 15W | Commercial Drones, Smart Cameras, Service Robots |
| **6** | **Raspberry Pi 5** | Broadcom BCM2712 | 4-core ARM Cortex-A76 | **0 TOPS** (ไม่มี NPU) | 2GB – 16GB LPDDR4X (17 GB/s) | 5W – 12W | Education, Maker/IoT Server, General Computing |
| **7** | **Khadas VIM4** | Amlogic A311D2 | 8-core (4x A73 + 4x A53) | **3.2 TOPS** (Amlogic NPU) | 8GB LPDDR4X | 5W – 12W | Smart Display, Digital Signage, Lightweight Vision |
| **8** | **STM32N6** | STM32N657 MCU | ARM Cortex-M55 (Helium) | **~0.6 – 3 TOPS** (Neural-ART) | 4.2 MB On-chip SRAM | **< 1W – 2W** | TinyML, Vibration Anomaly, Keyword Spotting |

---

# 🎯 คลังข้อสอบจำลอง: ชุดข้อสอบปรนัย (ข้อกา 20 ข้อ)

**คำชี้แจง**: เลือกคำตอบที่ถูกต้องที่สุดเพียงข้อเดียว พร้อมอ่านเฉลยและคำอธิบายเหตุผลด้านล่าง

### 1. ในการติดตั้ง Raspberry Pi OS ด้วย Raspberry Pi Imager เพื่อนำบอร์ดไปใช้งานแบบ Headless (ไม่ต่อจอภาพ) ข้อใดคือขั้นตอนที่สำคัญที่สุด?
* ก. ฟอร์แมตการ์ด MicroSD เป็นระบบไฟล์ NTFS ก่อนใช้งาน
* ข. แก้ไขค่าความถี่ CPU ในแถบ Advanced Configuration
* ค. กำหนด Username/Password, ตั้งค่า Wi-Fi และเปิดใช้งานบริการ SSH ในเมนู OS Customisation
* ง. เสียบสาย LAN เข้ากับพอร์ตเครือข่ายก่อนเริ่มเขียนข้อมูลลงการ์ด

### 2. หากต่อจอภาพเข้ากับบอร์ด Raspberry Pi 4 แล้วพบว่าหน้าจอไม่แสดงผลภาพตั้งแต่ขั้นตอนบูต ควรตรวจสอบข้อใดเป็นลำดับแรกตามคู่มือการใช้งาน?
* ก. ตรวจสอบว่าได้แก้ค่า `hdmi_mode` ในไฟล์ `config.txt` แล้วหรือไม่
* ข. ตรวจสอบว่าเสียบสายสัญญาณเข้าที่พอร์ต micro-HDMI 0 ซึ่งอยู่ติดกับพอร์ตจ่ายไฟ USB-C หรือไม่
* ค. ตรวจสอบว่าหน้าจอรองรับความละเอียด 8K หรือไม่
* ง. ถอดการ์ด MicroSD ออกมาล้างด้วยน้ำยาแอลกอฮอล์

### 3. หากเขียนข้อความในไฟล์ `cmdline.txt` ของ Raspberry Pi แยกเป็น 2 บรรทัด จะเกิดผลลัพธ์อย่างไร?
* ก. ระบบจะบูตเข้าสู่โหมด Safe Mode โดยอัตโนมัติ
* ข. ระบบจะทำงานเร็วขึ้นเนื่องจากแยกการอ่านพารามิเตอร์
* ค. บอร์ดจะไม่สามารถบูตระบบปฏิบัติการขึ้นมาได้
* ง. ระบบจะเปิดหน้าต่างเดสก์ท็อปขึ้นมา 2 หน้าจอ

### 4. บนระบบปฏิบัติการ Raspberry Pi OS รุ่นปัจจุบัน หากต้องการเรียกใช้โปรแกรมคีย์บอร์ดเสมือนบนหน้าจอ (Virtual Keyboard) เมื่อต่อจอสัมผัส ควรติดตั้งโปรแกรมใด?
* ก. Gboard
* ข. Squeekboard
* ค. SwiftKey
* ง. TouchType

### 5. จากผลการทดลองในรายงานการระบายความร้อน บอร์ด Raspberry Pi 4 จะเริ่มเกิดสภาวะ Thermal Throttling ที่อุณหภูมิประมาณเท่าใด และส่งผลกระทบอย่างไร?
* ก. 50°C และทำให้แรมล้น
* ข. 65°C และทำให้ภาพกระตุก 5%
* ค. 80°C และทำให้ Throughput ลดลงมากกว่า 35%
* ง. 100°C และทำให้บอร์ดระเบิดทันที

### 6. CPU ที่มี Address Bus ขนาด 24 บิต จะสามารถเข้าถึงตำแหน่งที่อยู่ของหน่วยความจำได้สูงสุดเท่าใด?
* ก. 64 KB
* ข. 1 MB
* ค. 16 MB
* ง. 4 GB

### 7. ในสถาปัตยกรรมคอมพิวเตอร์ การที่ CPU สามารถเขียนและอ่านค่าจากอุปกรณ์รอบข้าง (Peripherals) โดยใช้คำสั่งเดียวกับการอ่านเขียน Memory เรียกว่าอะไร?
* ก. Direct Memory Access (DMA)
* ข. Memory-Mapped I/O
* ค. Interrupt Service Routine
* ง. Cache Coherency

### 8. สัญญาณใดบนชิปหน่วยความจำที่มีหน้าที่เปิดให้ชิปนั้นสามารถรับส่งข้อมูลกับ Data Bus เมื่อ Address Decoder ถอดรหัสตำแหน่งตรงกับชิป?
* ก. RD (Read Enable)
* ข. WR (Write Enable)
* ค. CS (Chip Select)
* ง. CLK (Clock)

### 9. ข้อใดกล่าวถึงคุณสมบัติเด่น 3 ประการของ Convolutional Neural Network (CNN) ได้ถูกต้องที่สุด?
* ก. Global Attention, Recurrent Memory, Gated Cell
* ข. Local Receptive Fields, Shared Weights, Subsampling/Pooling
* ค. Random Forest, Hyperplane, Kernel Trick
* ง. Supervised Loss, Policy Gradient, Value Table

### 10. ภาพอินพุตขนาด $48 \times 48$ พิกเซล ผ่านชั้น Convolution ที่ใช้ Filter ขนาด $7 \times 7$, Stride = 2 และไม่มีการเติมขอบ (Padding = 0) จะได้ Feature Map ขนาดเท่าใด?
* ก. $20 \times 20$
* ข. $21 \times 21$
* ค. $22 \times 22$
* ง. $24 \times 24$

### 11. ชั้น Convolution ที่มี Kernel ขนาด $3 \times 3$, จำนวน Channel ขาเข้าเท่ากับ 8 และสร้าง Feature Maps ขาออกจำนวน 16 Channels จะมีจำนวน Parameter สำหรับการเทรนทั้งหมดกี่ตัว (รวม Bias)?
* ก. 144 ตัว
* ข. 1,152 ตัว
* ค. 1,168 ตัว
* ง. 2,320 ตัว

### 12. ในการออกแบบ Fully Connected Layer ของโครงข่าย CNN หากกำหนดจำนวนนิวรอนมากเกินไป (Too Many Neurons) จะส่งผลเสียตามข้อใด?
* ก. ทำให้โมเดลเกิด Underfitting
* ข. ทำให้การคำนวณรวดเร็วขึ้นแต่ความจำสั้น
* ค. ทำให้โมเดลเสี่ยงต่อการเกิด Overfitting และประมวลผลหนักเกินไป
* ง. ทำให้ Feature Map หดเล็กลงเหลือ 0

### 13. ลำดับขั้นตอนการทำงาน 5 เลเยอร์ของ Large Language Model (LLM) ข้อใดเรียงลำดับได้อย่างถูกต้อง?
* ก. Embedding $\to$ Tokenization $\to$ Transformer $\to$ Detokenization $\to$ Linear & Softmax
* ข. Tokenization $\to$ Embedding $\to$ Transformer $\to$ Linear & Softmax $\to$ Detokenization
* ค. Transformer $\to$ Tokenization $\to$ Softmax $\to$ Embedding $\to$ Output
* ง. Softmax $\to$ Transformer $\to$ Positional Encoding $\to$ Tokenization $\to$ EOS

### 14. ในกลไกของ LLM ส่วนใดทำหน้าที่คำนวณค่าน้ำหนักความสนใจเพื่อหาความสัมพันธ์ระหว่างคำแต่ละคำในประโยค?
* ก. Tokenizer
* ข. Self-Attention Mechanism
* ค. Softmax Layer
* ง. Detokenizer

### 15. ในสถาปัตยกรรมของ YOLOv5 ข้อใดคือความแตกต่างสำคัญของชั้น Input Layer เมื่อเทียบกับ YOLOv4?
* ก. YOLOv5 ใช้ MaxPooling $2\times2$ ทันที
* ข. YOLOv5 ใช้ Slice Layer หั่นรูปเป็น 4 patches แบบ Interleave $2\times2$ เพื่อรักษาข้อมูลพิกเซลครบถ้วน
* ค. YOLOv5 ลดขนาดภาพเหลือ $224\times224$ ด้วย Bilinear Interpolation
* ง. YOLOv5 ใช้ Fast Fourier Transform แปลงภาพเข้าโดเมนความถี่

### 16. โมเดล YOLOv5 ที่รับภาพขนาด $640 \times 640$ พิกเซล จะสร้าง Bounding Box ขาออกรวมทุกสเกลเป็นจำนวนทั้งหมดเท่าใดต่อ 1 ภาพ?
* ก. 1,000 กล่อง
* ข. 8,400 กล่อง
* ค. 25,200 กล่อง
* ง. 80,000 กล่อง

### 17. โครงสร้าง SPPF (Spatial Pyramid Pooling Fast) ใน YOLOv5 ได้รับการพัฒนาให้เหนือกว่า SPP ใน YOLOv4 อย่างไร?
* ก. ยกเลิกการทำ MaxPool แล้วเปลี่ยนไปใช้ Average Pool แทน
* ข. เปลี่ยนจากการคำนวณ MaxPool ขนาด 5, 9, 13 แบบขนาน มาเป็นการต่อ MaxPool $5\times5$ แบบอนุกรม 3 รอบ ซึ่งได้ผลลัพธ์เท่าเดิมแต่คำนวณเร็วกว่าเกือบเท่าตัว
* ค. ใช้ Convolution $1\times1$ เข้ามาแทนที่การทำ Pooling ทั้งหมด
* ง. ลดจำนวนแชนแนลลง 90% ก่อนส่งเข้าคอขวด

### 18. โมเดลประเภทใดที่ออกแบบมาเพื่อแก้ไขปัญหา Vanishing Gradient ของ RNN โดยใช้ Cell State เป็นทางด่วนความจำ ร่วมกับ Forget, Input และ Output Gate?
* ก. Transformer
* ข. LSTM
* ค. GRU
* ง. Decision Tree

### 19. หากต้องการพัฒนาระบบ Predictive Maintenance เพื่อตรวจจับความผิดปกติจากการสั่นสะเทือนของมอเตอร์ในโรงงาน โดยใช้พลังงานจากแบตเตอรี่ก้อนเล็กเป็นเวลา 1 ปี บอร์ดใดในตารางมีความเหมาะสมที่สุด?
* ก. NVIDIA IGX Thor
* ข. Raspberry Pi 5
* ค. STM32N6 (STM32N657)
* ง. Khadas VIM4

### 20. บอร์ดคู่ใดต่อไปนี้ให้พลังประมวลผล AI สูงระดับ 200–275 TOPS แต่มีอัตราการบริโภคพลังงาน (TDP) เพียง 15W–60W ทำให้เหมาะสมที่สุดสำหรับติดตั้งบนหุ่นยนต์เคลื่อนที่อัตโนมัติ (AMR) และหุ่นยนต์ฮิวแมนนอยด์?
* ก. Raspberry Pi 5 และ Khadas VIM4
* ข. NVIDIA Jetson AGX Orin
* ค. Orange Pi 5 Plus
* ง. STM32N6

---

## 🔑 เฉลยคำตอบข้อสอบปรนัยพร้อมคำอธิบาย

1. **เฉลย ค.** ในการใช้งาน Headless ต้องเปิดบริการ SSH และใส่รหัสผ่าน/Wi-Fi ล่วงหน้าในหน้า OS Customisation เพื่อให้สามารถรีโมทสั่งการผ่านเครือข่ายได้ทันทีโดยไม่ต้องต่อจอ
2. **เฉลย ข.** Raspberry Pi 4 มีช่องต่อจอ 2 ช่อง พอร์ต micro-HDMI 0 (ติดกับ USB-C) เป็นพอร์ตหลักที่แสดงผลตอนเริ่มบูตระบบ หากเสียบช่อง 1 จออาจไม่ติด
3. **เฉลย ค.** ไฟล์ `cmdline.txt` เป็นคำสั่ง Boot Arguments ของเคอร์เนล Linux กฎเหล็กคือต้องอยู่บรรทัดเดียวเท่านั้น หากขึ้นบรรทัดใหม่เครื่องจะไม่สามารถบูตได้
4. **เฉลย ข.** Squeekboard เป็นโปรแกรมคีย์บอร์ดบนหน้าจอมาตรฐานของระบบ Raspberry Pi OS รุ่นปัจจุบัน
5. **เฉลย ค.** จากผลการทดสอบ RPi 4 เริ่ม Throttling ที่ ~80°C และหากไม่มีพัดลมจะลดความเร็วลงจน Throughput ร่วงเกิน 35%
6. **เฉลย ค.** คำนวณจาก $2^{24} = 16,777,216\text{ Bytes} = 16\text{ MB}$
7. **เฉลย ข.** Memory-Mapped I/O เป็นสถาปัตยกรรมที่แมปอุปกรณ์รอบข้างให้เป็นส่วนหนึ่งของพื้นที่หน่วยความจำ
8. **เฉลย ค.** สัญญาณ Chip Select (CS) จะถูกส่งมาจาก Address Decoder เพื่อสั่งเปิดการทำงานของชิปตัวนั้นๆ
9. **เฉลย ข.** จุดเด่นหลัก 3 อย่างของ CNN ตามนิยามในบทเรียนคือ Local Receptive Fields, Shared Weights และ Subsampling/Pooling
10. **เฉลย ข.** เข้าสูตร: $W_{\text{out}} = \lfloor \frac{48 - 7 + 0}{2} \rfloor + 1 = \lfloor \frac{41}{2} \rfloor + 1 = 20 + 1 = 21$
11. **เฉลย ค.** คำนวณจาก $(3 \times 3 \times 8 + 1) \times 16 = (72 + 1) \times 16 = 73 \times 16 = 1,168$ ตัว
12. **เฉลย ค.** การมีนิวรอนมากเกินไปทำให้เกิด Overfitting โมเดลจะจำข้อมูลชุดฝึกมากกว่าเรียนรู้ความสัมพันธ์ทั่วไป และทำให้ระบบกินแรม/ประมวลผลช้า
13. **เฉลย ข.** ลำดับที่ถูกต้องตามใบงานในห้องเรียน: Tokenization $\to$ Embedding $\to$ Transformer $\to$ Linear & Softmax $\to$ Detokenization
14. **เฉลย ข.** Self-Attention คือกลไกที่คำนวณ Matrix การกระจายน้ำหนักความสนใจระหว่างคู่คำทั้งหมด
15. **เฉลย ข.** YOLOv5 ใช้ Slice Layer ตัดแบ่งรูปเป็น 4 patches ขนาด $(12, 320, 320)$ โดยไม่สูญเสียข้อมูลพิกเซล
16. **เฉลย ค.** รวมจาก 3 สเกล: $(80^2 + 40^2 + 20^2) \times 3 = (6,400 + 1,600 + 400) \times 3 = 8,400 \times 3 = 25,200$ กล่อง
17. **เฉลย ข.** SPPF ใช้ MaxPool $5\times5$ ต่ออนุกรม 3 ครั้ง ได้ผลลัพธ์เท่ากับ SPP (MaxPool 5, 9, 13 ขนาน) แต่คำนวณเร็วกว่าเกือบ 2 เท่า
18. **เฉลย ข.** LSTM มี Cell State ทำหน้าที่เป็นสายพานความจำระยะยาว ควบคุมด้วย 3 Gate
19. **เฉลย ค.** STM32N6 เป็นระดับไมโครคอนโทรลเลอร์ (MCU) กินไฟต่ำกว่า 1-2 วัตต์ มี NPU ในตัว เหมาะสำหรับงาน TinyML ตรวจการสั่นสะเทือน
20. **เฉลย ข.** NVIDIA Jetson AGX Orin ให้พลัง 200–275 TOPS กินไฟเพียง 15–60W จึงเหมาะสมที่สุดสำหรับหุ่นยนต์ที่ขับเคลื่อนด้วยแบตเตอรี่

---

# ✍️ คลังข้อสอบจำลอง: ชุดข้อสอบอัตนัย (ข้อเขียน 6 ข้อใหญ่)

### 📝 ข้อที่ 1: การคำนวณ Convolution และ Max Pooling ด้วยมือ (10 คะแนน)

กำหนดให้อินพุตภาพแบบ Grayscale ขนาด $5 \times 5$ พิกเซล และ Kernel $K$ ขนาด $3 \times 3$ ดังต่อไปนี้:

$$\text{Input } X = \begin{bmatrix} 4 & 3 & 2 & 1 & 0 \\ 3 & 4 & 3 & 2 & 1 \\ 2 & 3 & 5 & 3 & 2 \\ 1 & 2 & 3 & 4 & 3 \\ 0 & 1 & 2 & 3 & 4 \end{bmatrix}, \quad \text{Kernel } K = \begin{bmatrix} 1 & 0 & -1 \\ 0 & 1 & 0 \\ -1 & 0 & 1 \end{bmatrix}$$

โดยกำหนดให้ไม่มีการเติมขอบ (Padding $P=0$) และเลื่อนสแกนทีละ 1 พิกเซล (Stride $S=1$)
1. จงแสดงการคำนวณหาขนาดมิติของ Feature Map ขาออก
2. จงแสดงวิธีคำนวณหาค่าพิกเซลของ Feature Map ที่ตำแหน่ง $(1,1), (1,2)$ และ $(2,2)$
3. หากนำ Feature Map ขนาด $3 \times 3$ ที่ได้ มาทำการคำนวณ Max Pooling ขนาด $2 \times 2$ (Stride $S=1$) จงหาค่าผลลัพธ์ที่ตำแหน่งแรก $(1,1)$

#### 💡 แนวทางคำตอบและวิธีทำ:
1. **คำนวณขนาด Feature Map**:

   $$W_{\text{out}} = \left\lfloor \frac{W_{\text{in}} - K + 2P}{S} \right\rfloor + 1 = \frac{5 - 3 + 0}{1} + 1 = \mathbf{3 \times 3}$$

2. **คำนวณค่าตำแหน่งพิกเซล (Element-wise Multiplication & Sum)**:

   * **ตำแหน่ง $(1,1)$**: ครอบแถวที่ 1–3 และคอลัมน์ที่ 1–3:

     $$\text{Sub-matrix} = \begin{bmatrix} 4 & 3 & 2 \\ 3 & 4 & 3 \\ 2 & 3 & 5 \end{bmatrix}$$

     $$\text{Value} = (4\cdot1) + (3\cdot0) + (2\cdot(-1)) + (3\cdot0) + (4\cdot1) + (3\cdot0) + (2\cdot(-1)) + (3\cdot0) + (5\cdot1) = 4 - 2 + 4 - 2 + 5 = \mathbf{9}$$

   * **ตำแหน่ง $(1,2)$**: ครอบแถวที่ 1–3 และคอลัมน์ที่ 2–4:

     $$\text{Sub-matrix} = \begin{bmatrix} 3 & 2 & 1 \\ 4 & 3 & 2 \\ 3 & 5 & 3 \end{bmatrix}$$

     $$\text{Value} = (3\cdot1) + (1\cdot(-1)) + (3\cdot1) + (3\cdot(-1)) + (3\cdot1) = 3 - 1 + 3 - 3 + 3 = \mathbf{5}$$

   * **ตำแหน่ง $(2,2)$**: ครอบแถวที่ 2–4 และคอลัมน์ที่ 2–4:

     $$\text{Sub-matrix} = \begin{bmatrix} 4 & 3 & 2 \\ 3 & 5 & 3 \\ 2 & 3 & 4 \end{bmatrix}$$

     $$\text{Value} = (4\cdot1) + (2\cdot(-1)) + (5\cdot1) + (2\cdot(-1)) + (4\cdot1) = 4 - 2 + 5 - 2 + 4 = \mathbf{9}$$

3. **การทำ Max Pooling ($2 \times 2, S=1$) ที่ตำแหน่ง $(1,1)$**:
   * นำ 4 ค่าแรกของบล็อก $2 \times 2$ บนซ้าย ได้แก่ ตำแหน่ง $(1,1)=9, (1,2)=5$ และสมมติค่า $(2,1), (2,2)=9$:
   * ค่าสูงสุดในบล็อก: $\max(9, 5, \text{val}_{21}, 9) = \mathbf{9}$

---

### 📝 ข้อที่ 2: การคำนวณโครงสร้างเครือข่าย CNN ตลอดทั้งสาย (10 คะแนน)
โครงข่าย CNN รับภาพสี RGB ขนาด $128 \times 128 \times 3$ ผ่านลำดับชั้นการทำงานดังนี้:
* **Layer 1 (Conv1)**: Kernel ขนาด $5 \times 5$, Padding = 2, Stride = 2, จำนวน Filter = 32
* **Layer 2 (Pool1)**: Max Pooling ขนาด $2 \times 2$, Stride = 2
* **Layer 3 (Conv2)**: Kernel ขนาด $3 \times 3$, Padding = 1, Stride = 1, จำนวน Filter = 64
* **Layer 4 (Pool2)**: Max Pooling ขนาด $2 \times 2$, Stride = 2
* **Layer 5 (Dense/FC)**: เชื่อมต่อไปยัง Fully Connected Layer ที่มี 128 นิวรอน
1. จงคำนวณขนาด Output Dimension ของข้อมูลหลังผ่านแต่ละ Layer
2. จงคำนวณจำนวน Parameter ทั้งหมดใน Layer 1 (Conv1)
3. จงคำนวณจำนวนโหนดทั้งหมดหลังจากการทำ Flatten ก่อนเข้าสู่ Layer 5

#### 💡 แนวทางคำตอบและวิธีทำ:
1. **คำนวณ Output Dimension แต่ละชั้น**:
   * **Layer 1 (Conv1)**:
     $$W_1 = \left\lfloor \frac{128 - 5 + 2(2)}{2} \right\rfloor + 1 = \left\lfloor \frac{127}{2} \right\rfloor + 1 = 63 + 1 = 64 \implies \mathbf{64 \times 64 \times 32}$$
   * **Layer 2 (Pool1)**:
     $$W_2 = \frac{64}{2} = 32 \implies \mathbf{32 \times 32 \times 32}$$
   * **Layer 3 (Conv2)**:
     $$W_3 = \left\lfloor \frac{32 - 3 + 2(1)}{1} \right\rfloor + 1 = 31 + 1 = 32 \implies \mathbf{32 \times 32 \times 64}$$
   * **Layer 4 (Pool2)**:
     $$W_4 = \frac{32}{2} = 16 \implies \mathbf{16 \times 16 \times 64}$$
2. **คำนวณ Parameters ของ Layer 1**:
   $$\text{Params} = (K_w \times K_h \times C_{\text{in}} + 1) \times C_{\text{out}} = (5 \times 5 \times 3 + 1) \times 32 = (75 + 1) \times 32 = \mathbf{2,432\text{ parameters}}$$
3. **จำนวนโหนดหลังทำ Flatten**:
   $$\text{Total Nodes} = 16 \times 16 \times 64 = \mathbf{16,384\text{ โหนด}}$$

---

### 📝 ข้อที่ 3: การคำนวณ Forward Propagation ของ Single Hidden Layer MLP (10 คะแนน)
กำหนดโครงข่ายประสาทเทียมแบบ Multi-Layer Perceptron (MLP) ดังนี้:
* **อินพุต**: $x_1 = 2.0, \quad x_2 = -1.0$, กำหนด Bias ขาเข้า $b_{\text{in}} = 1.0$
* **ค่าน้ำหนักชั้น Input $\to$ Hidden**:
  * โหนดที่ 1 ($h_1$): $w_{11} = 0.5, \quad w_{12} = -0.4, \quad b_1 = 0.2$
  * โหนดที่ 2 ($h_2$): $w_{21} = -0.8, \quad w_{22} = 0.6, \quad b_2 = -0.5$
  * กำหนดฟังก์ชันกระตุ้นที่ Hidden Layer เป็น **ReLU** ($f(z) = \max(0, z)$)
* **ค่าน้ำหนักชั้น Hidden $\to$ Output**:
  * โหนดขาออก ($y$): $w_1 = 1.5, \quad w_2 = -1.0$, กำหนด Bias ชั้น Hidden $b_{\text{hid}} = 1.0$ มีค่าน้ำหนัก Bias $w_b = 0.4$ (ใช้ Linear Activation)
จงแสดงวิธีทำเพื่อหาค่าเอาต์พุต $y$ ของระบบ

#### 💡 แนวทางคำตอบและวิธีทำ:
1. **คำนวณผลรวมที่ Hidden Layer**:
   * โหนด $h_1$:
     $$z_1 = (w_{11} \cdot x_1) + (w_{12} \cdot x_2) + (b_1 \cdot b_{\text{in}}) = (0.5 \times 2.0) + (-0.4 \times -1.0) + (0.2 \times 1.0)$$
     $$z_1 = 1.0 + 0.4 + 0.2 = \mathbf{1.6}$$
     ผ่าน $\text{ReLU} \implies a_1 = \max(0, 1.6) = \mathbf{1.6}$
   * โหนด $h_2$:
     $$z_2 = (w_{21} \cdot x_1) + (w_{22} \cdot x_2) + (b_2 \cdot b_{\text{in}}) = (-0.8 \times 2.0) + (0.6 \times -1.0) + (-0.5 \times 1.0)$$
     $$z_2 = -1.6 - 0.6 - 0.5 = \mathbf{-2.7}$$
     ผ่าน $\text{ReLU} \implies a_2 = \max(0, -2.7) = \mathbf{0.0}$
2. **คำนวณค่า Output $y$**:
   $$y = (w_1 \cdot a_1) + (w_2 \cdot a_2) + (w_b \cdot b_{\text{hid}})$$
   $$y = (1.5 \times 1.6) + (-1.0 \times 0.0) + (0.4 \times 1.0) = 2.4 + 0 + 0.4 = \mathbf{2.80}$$

---

### 📝 ข้อที่ 4: การทำงาน 5 เลเยอร์ของ LLM และการนำไปรันบน Edge (10 คะแนน)
1. จงอธิบายหลักการทำงานของ Large Language Model (LLM) ครบทั้ง 5 เลเยอร์ตามที่ได้ศึกษาในห้องเรียน พร้อมวาดแผนผังการไหลของข้อมูล (Workflow)
2. อธิบายว่าเหตุใดโมเดลภาษาขนาดใหญ่จึงรันบนอุปกรณ์ขนาดเล็ก (Edge Device) ได้ยาก และเทคนิค **Quantization (เช่น INT4/INT8)** ช่วยแก้ปัญหานี้ได้อย่างไร

#### 💡 แนวทางคำตอบและวิธีทำ:
1. **การทำงาน 5 เลเยอร์ของ LLM**:
   * **1. Tokenization**: หั่นข้อความตัวหนังสือออกเป็นหน่วยย่อย (Token) และแปลงเป็นรหัสตัวเลข (Token ID) ตามตาราง Vocabulary
   * **2. Embedding**: แมป Token ID เป็นเวกเตอร์ความหมายหลายมิติ (Word Vector) พร้อมบวกค่า Positional Encoding เพื่อระบุตำแหน่งคำในประโยค
   * **3. Transformer Block**: ประมวลผลผ่าน Self-Attention เพื่อคำนวณค่าน้ำหนักเชื่อมโยงความสัมพันธ์ของคำทุกคำในประโยค แล้วส่งผ่าน Feed-Forward Network (FFN) สกัดฟีเจอร์ความหมายเชิงลึก
   * **4. Linear & Softmax**: ขยายเวกเตอร์เข้าสมการ Linear ให้มิติเท่ากับ Vocab Size เพื่อได้คะแนนดิบ (Logits) แล้วส่งผ่าน Softmax แปลงเป็นค่าความน่าจะเป็นเพื่อเลือก Token ID ถัดไป
   * **5. Detokenization**: แปลง Token ID ที่ทำนายได้กลับมาเป็นข้อความ และทำการวนลูป (Autoregressive Loop) ส่งกลับไปต่อท้ายอินพุตเพื่อทำนายคำถัดไปจนกว่าจะพบสัญญาณหยุด (EOS Token)
   * *แผนผังการไหล*:
     $$\text{Input Text} \to \text{Tokenization} \to \text{Embedding} \to \text{Transformer} \to \text{Linear+Softmax} \to \text{Detokenization} \to \text{Output} \to \text{วนลูป}$$
2. **ปัญหาและการนำไปรันบน Edge**:
   * **สาเหตุที่รันยาก**: โมเดล LLM มีขนาดพารามิเตอร์ระดับพันล้านตัว (เช่น 7B) ที่ Precision ปกติ (FP16/32) ต้องใช้ RAM มหาศาลกว่า 14 GB และติดคอขวดที่ความเร็วการอ่านแรม (Memory Bandwidth Bound) เพราะต้องดึงน้ำหนักทั้งหมดมาคำนวณทุกๆ 1 Token
   * **การแก้ด้วย Quantization**: บีบอัดตัวเลขน้ำหนักจาก Float 16-bit เหลือเป็น Integer 4-bit (INT4) หรือ 8-bit (INT8) ช่วยลดขนาดการใช้ RAM ของโมเดล 7B ลงจาก 14 GB เหลือเพียง ~4–5 GB ทำให้สามารถโหลดขึ้นแรมของบอร์ด Edge (เช่น Jetson Orin หรือ Raspberry Pi 5) และประมวลผลคำนวณด้วยชุดคำสั่ง Integer ได้อย่างรวดเร็ว

---

### 📝 ข้อที่ 5: สถาปัตยกรรม YOLOv4 vs YOLOv5 และกลไก NMS (10 คะแนน)
1. จงเปรียบเทียบจุดเด่นของสถาปัตยกรรม **YOLOv5** ที่ได้รับการพัฒนาเหนือกว่า **YOLOv4** ใน 3 ประเด็น: (1) Input Layer, (2) Activation Function และ (3) Spatial Pooling
2. อธิบายกลไกการทำงานของ **Non-Maximum Suppression (NMS)** ในขั้นตอนตรวจจับวัตถุ พร้อมระบุว่าสูตร **IoU (Intersection over Union)** มีความสำคัญอย่างไรในการตัดกล่องที่ซ้ำซ้อน

#### 💡 แนวทางคำตอบและวิธีทำ:
1. **การเปรียบเทียบ YOLOv4 vs YOLOv5**:
   * *(1) Input Layer*: YOLOv4 ใช้ Conv2D $3\times3$ ตามปกติ แต่ YOLOv5 ใช้ **Focus / Slice Layer** หั่นภาพแบบ Interleave $2\times2$ เป็น 4 Patches ช่วยเพิ่ม Channel เป็น 12 โดยเก็บรายละเอียดข้อมูลพิกเซลได้ครบถ้วนโดยไม่ต้องลดความละเอียดภาพทิ้ง
   * *(2) Activation Function*: YOLOv4 ใช้ Mish ซึ่งคำนวณฟังก์ชันเลขชี้กำลังซับซ้อน แต่ YOLOv5 ใช้ **SiLU (Swish)** ที่คำนวณได้เร็วกว่า มีความโค้งมนราบเรียบ ทำให้ Gradient ไหลผ่านได้ดีกว่าและเสถียรกว่า
   * *(3) Spatial Pooling*: YOLOv4 ใช้ **SPP** แบบขนาน (คำนวณ MaxPool $5, 9, 13$ แยกสายกันแล้วนำมาต่อกัน) แต่ YOLOv5 ใช้ **SPPF** ทำ MaxPool $5\times5$ อนุกรมต่อกัน 3 ขั้น ซึ่งให้ผลลัพธ์ทางคณิตศาสตร์เท่ากับ SPP แต่มีความเร็วในการประมวลผลสูงกว่าเกือบ 2 เท่า
2. **กลไก NMS และ IoU**:
   * **สูตร IoU**: $\text{IoU} = \frac{\text{Area of Overlap}}{\text{Area of Union}} = \frac{A \cap B}{A \cup B}$ ใช้วัดสัดส่วนพื้นที่ทับซ้อนกันระหว่าง Bounding Box สองกล่อง
   * **ขั้นตอนของ NMS**:
     1. รวบรวม Bounding Box ทั้งหมดที่ผ่านเกณฑ์ความเชื่อมั่น แล้วนำมาจัดเรียงตาม **Confidence Score จากมากไปน้อย**
     2. เลือกกล่องที่มีคะแนนสูงสุดไว้เป็นกล่องตัวแทนหลักของวัตถุนั้น
     3. นำกล่องตัวแทนไปคำนวณค่า IoU เทียบกับกล่องที่เหลือทั้งหมด หากกล่องใดมีค่า $\text{IoU} > \text{Threshold}$ (เช่น $0.5$) แสดงว่าเป็นกล่องตรวจจับวัตถุชิ้นเดียวกันที่ซ้ำซ้อน $\implies$ **สั่งลบกล่องนั้นทิ้งทันที**
     4. ทำซ้ำตามลำดับจนครบ ทำให้เหลือกล่องที่แม่นยำที่สุดเพียง 1 กล่องต่อวัตถุ 1 ชิ้น

---

### 📝 ข้อที่ 6: การคำนวณภาระงาน (Workload Capacity) และการเลือกระบบบอร์ด Edge AI (10 คะแนน)
ระบบหุ่นยนต์ตรวจสอบความปลอดภัยในโรงงานอุตสาหกรรม มีภาระงานประมวลผลโมเดล AI พร้อมกัน 3 งานดังนี้:
* **งานที่ 1**: โมเดลตรวจจับคนและ PPE (YOLOv8s) ใช้ 28.6 GOPs ต่อเฟรม รันที่ 30 FPS จำนวน 2 กล้อง
* **งานที่ 2**: โมเดลตรวจจับความผิดปกติของเครื่องจักร (3D Anomaly Net) ใช้ 200 GOPs รันที่ 10 FPS
* **งานที่ 3**: โมเดลจดจำท่าทางคน (Pose Estimation) ใช้ 40 GOPs รันที่ 30 FPS
1. จงคำนวณหาพลังการประมวลผล AI รวมที่ระบบต้องการ (Required TOPS)
2. หากมีตัวเลือกบอร์ด 3 ตัว ได้แก่:
   * (A) **Raspberry Pi 5** (0 TOPS NPU ในตัว, TDP 5W–12W)
   * (B) **Orange Pi 5** (6 TOPS NPU, TDP 5W–15W)
   * (C) **NVIDIA Jetson AGX Orin** (200–275 TOPS, TDP 15W–60W)
   จงวิเคราะห์ว่าบอร์ดใดสามารถรองรับระบบนี้ได้อย่างมีประสิทธิภาพ พร้อมให้เหตุผลทางวิศวกรรม
3. หากเลือกใช้บอร์ดตัวที่ผ่านเกณฑ์ แล้วนำไปติดตั้งบนหุ่นยนต์ที่ใช้แบตเตอรี่ $24\text{V}, 15\text{Ah}$ โดยบอร์ดกินไฟเฉลี่ย $40\text{W}$ (วงจรแปลงไฟมีประสิทธิภาพ $\eta = 0.85$) หุ่นยนต์ตัวนี้จะสามารถปฏิบัติงานได้ต่อเนื่องกี่ชั่วโมง?

#### 💡 แนวทางคำตอบและวิธีทำ:
1. **คำนวณ Required TOPS แต่ละงาน**:
   * งานที่ 1 (2 กล้อง): $\frac{(2 \times 28.6) \times 30}{1,000} = \frac{1,716}{1,000} = \mathbf{1.716\text{ TOPS}}$
   * งานที่ 2: $\frac{200 \times 10}{1,000} = \frac{2,000}{1,000} = \mathbf{2.000\text{ TOPS}}$
   * งานที่ 3: $\frac{40 \times 30}{1,000} = \frac{1,200}{1,000} = \mathbf{1.200\text{ TOPS}}$
   * **รวม Required TOPS ทั้งหมด**:
     $$\text{Total Required TOPS} = 1.716 + 2.000 + 1.200 = \mathbf{4.916\text{ TOPS}}$$
2. **การวิเคราะห์การเลือกระบบบอร์ด**:
   * **(A) Raspberry Pi 5 (0 TOPS)**: **ไม่ผ่านเกณฑ์** เนื่องจากไม่มี NPU ในตัว การรันทั้ง 3 โมเดลบน CPU จะทำให้เกิด CPU Overload 100% เครื่องค้างและเฟรมเรตร่วงเหลือ < 1 FPS
   * **(B) Orange Pi 5 (6 TOPS)**: **ไม่แนะนำสำหรับการใช้งานจริง** แม้จะมี 6 TOPS ตามสเปกกระดาษ (ภาระงาน 4.916 TOPS คิดเป็น ~82% ของชิป) แต่ประสิทธิภาพการทำงานจริง (Hardware Efficiency) ของ NPU ทั่วไปอยู่ที่ประมาณ 50–60% ทำให้พลังงานจริงได้เพียง ~3.0–3.6 TOPS จึงเกิดปัญหาคอขวดและ Frame Drop รุนแรง
   * **(C) NVIDIA Jetson AGX Orin (200–275 TOPS)**: ⭐ **เหมาะสมและผ่านเกณฑ์ที่สุด** ภาระงาน 4.916 TOPS คิดเป็นเพียง **~1.8% – 2.5%** ของขีดความสามารถบอร์ด ทำให้มี Headroom เหลือมากกว่า 97% สามารถรันทั้ง 3 งานพร้อมกันแบบ Real-time และยังมีสถาปัตยกรรม Ampere GPU + NVDLA ช่วยแบ่งเบาภาระงาน Vision ได้อย่างสมบูรณ์แบบ
3. **คำนวณระยะเวลาใช้งานแบตเตอรี่ (Battery Runtime)**:
   * ความจุพลังงานของแบตเตอรี่:
     $$\text{Energy (Wh)} = \text{Capacity (Ah)} \times \text{Voltage (V)} = 15\text{ Ah} \times 24\text{ V} = \mathbf{360\text{ Wh}}$$
   * ระยะเวลาที่ระบบทำงานได้:
     $$\text{Runtime} = \frac{\text{Energy (Wh)} \times \eta}{P_{\text{system}}} = \frac{360 \times 0.85}{40} = \frac{306}{40} = \mathbf{7.65\text{ ชั่วโมง}} \quad (\approx 7\text{ ชั่วโมง } 39\text{ นาที})$$
