# Ev3-Face-detect

This project enables **real-time face tracking using a webcam and an EV3 robot**. The EV3 runs **ev3dev** (or any OS supporting Python on EV3), while the PC handles **live face detection with OpenCV** and controls the EV3 motors to point at detected faces.

## 🚀 Features
- **Live face detection using OpenCV** on the PC.
- **Real-time motor control** via WebSockets.
- **Automatic device discovery** using mDNS (no need to manually enter IPs).
- **Compatible with EV3 running ev3dev or similar Linux-based OS.**
- **PC-side face detection processing** using OpenCV.

---

## 📌 Requirements
### **On the EV3:**
- **ev3dev** or any OS that can run Python.
- **Python 3.7+**
- **Required Python libraries:**
  ```sh
  pip3 install websockets ev3dev2 zeroconf
  ```

### **On the PC:**
- **Python 3.7+**
- **Webcam** for face detection.
- **OpenCV installed:**
  ```sh
  pip install opencv-python websockets zeroconf
  ```

---

## ⚙️ Setup
### **1️⃣ Start WebSocket Server on PC**
```sh
python3 face_tracking_websocket_server.py
```
This will:
- Start a WebSocket server on port **8765**.
- Automatically announce the server using **mDNS** for auto-discovery by the EV3.
- Detect faces using OpenCV and send coordinates to the EV3.

### **2️⃣ Start WebSocket Client on EV3**
```sh
python3 ev3_websocket_client.py
```
This will:
- Auto-discover the WebSocket server using **mDNS**.
- Receive face position data and control **motors** to track the detected face.

---

## 🔄 How It Works
1. **EV3 connects** to the PC WebSocket server.
2. **PC captures webcam feed** and detects faces using **OpenCV**.
3. **PC calculates the face position** and sends motor control signals to the EV3.
4. **EV3 adjusts motors** to point at the detected face.

---

## 🛠 Troubleshooting
### **WebSocket connection issues?**
- Ensure both devices are on the **same network**.
- Run `ifconfig` (Linux/macOS) or `ipconfig` (Windows) to find your **PC IP address**.
- Manually set the EV3 WebSocket connection if auto-discovery fails:
  ```python
  EV3_IP = "192.168.x.x"  # Replace with PC IP
  ````

### **Face detection not working?**
- Ensure your webcam is connected and working:
  ```sh
  python -c "import cv2; print(cv2.VideoCapture(0).isOpened())"
  ```
- Try running a manual test:
  ```sh
  python3 test_face_detection.py
  ```

---

## 📜 License
This project is licensed under the **Apache 2.0 License**. See the `LICENSE` file for details.

---

## 🔮 Future Plans
- ✅ **Optimize face tracking for faster response times.**
- ✅ **Improve motor movement accuracy based on face position.**
- 🛠 **Explore multi-face tracking and object recognition.**

---

## 🤝 Contributing
Contributions are welcome! If you have suggestions, **open an issue or submit a pull request**.

**Author:** Ludwig Bischoff

🌟 *If you like this project, consider starring it on GitHub!*

