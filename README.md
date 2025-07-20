# miniproject

# 🛰️ Animal Detection and Repulsion System

This project integrates **real-time animal detection** using **YOLOv8** with an **ultrasonic frequency-based animal repulsion system** built on a **PIC16F72 microcontroller**.

The goal is to detect animals through a camera feed and repel them using species-specific high-frequency sounds.

---

## 📦 Project Structure

```
animal-detection-repulsion/
├── yolo_tracker.py          # Python code for real-time detection using YOLOv8
├── pic_code/                # Embedded C code for PIC16F72 microcontroller
│   ├── main.c               # Logic for frequency generation based on animal type
│   ├── delay.c              # Delay utilities
│   ├── delay.h              # Header for delay functions
└── README.md                # Project description and instructions
```

---

## 🧠 Technologies Used

| Component     | Tech/Tool            |
|---------------|----------------------|
| Detection     | YOLOv8 (Ultralytics) |
| Platform      | Python, OpenCV       |
| Hardware      | Raspberry Pi 5       |
| Repulsion     | PIC16F72 Microcontroller |
| Frequency     | PWM via CCP module   |
| IDEs          | MPLAB X IDE, VS Code |
| Comms         | GPIO triggering from Pi to PIC |

---

## 🐾 Detection and Repulsion Logic

Each animal is detected using YOLOv8. When identified, a signal is sent from the Raspberry Pi to the PIC microcontroller, which generates a PWM signal at a species-specific frequency:

| Animal    | GPIO Pin (RAx) | Repulsion Frequency |
|-----------|----------------|---------------------|
| Elephant  | RA0            | 25 kHz              |
| Deer      | RA1            | 35 kHz              |
| Monkey    | RA2            | 27 kHz              |
| Dog       | RA3            | 40 kHz              |

Each signal lasts ~30 seconds using Timer0 interrupt.

---

## 🐍 YOLOv8 Python Script

- Loads a trained YOLOv8 model (`best.pt`)
- Captures webcam input using OpenCV
- Detects animals and annotates frames
- Sends GPIO signal based on class detected
- Press `q` to stop the video stream

> 📁 File: `yolo_tracker.py`

---

## 🔧 PIC16F72 Embedded Code

- **`main.c`**: Reads GPIO input from Raspberry Pi and outputs PWM using CCP module
- **`delay.c` / `delay.h`**: Millisecond delay utilities for signal stability
- Uses `TMR0` to time buzzer off after 30s

> 📁 Folder: `pic_code/`

---

## 🚀 Getting Started

### 1. Clone the Repo
```bash
git clone https://github.com/<your-username>/animal-detection-repulsion.git
cd animal-detection-repulsion
```

### 2. Python Setup (YOLOv8)
```bash
pip install ultralytics opencv-python
```

### 3. Run the Tracker
```bash
python yolo_tracker.py
```

### 4. Embedded Setup
- Load `main.c`, `delay.c`, and `delay.h` into MPLAB X IDE.
- Compile and flash to PIC16F72 using a programmer (e.g., PICkit 3).

---

## 📸 Example Use Case

1. Raspberry Pi detects a monkey via webcam.
2. GPIO RA2 on PIC goes high.
3. PIC generates a 27 kHz tone via PWM for 30 seconds.
4. Monkey leaves the area due to discomfort.

---

## 💡 Future Improvements

- Add GPS-based location tagging
- Enable drone flight to detection site
- Record detection logs in cloud database

---

## 📜 License

This project is open-source and free to use for research and education purposes.

---

## 🙋‍♀️ Author

**Hiba Beeran**  
📍 Kochi, Kerala  
🔗 [LinkedIn](https://www.linkedin.com/in/hiba-beeran-b4504725a)
