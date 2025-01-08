# 🔐 SBD Encryption Project

Still adding screenshots...

## 📝 Objective
The goal of this project is to demonstrate how to establish a secure connection between a **Kali Linux VM** and a **Windows VM** using **SBD (Secure Backdoor)**. The project also involves capturing and analyzing network traffic using **Wireshark** to verify that the connection is encrypted by default.

---

## 🛠️ Skills Learned
- Setting up secure connections using SBD
- Transferring files between Kali and Windows VMs
- Using Wireshark to capture and analyze network traffic
- Troubleshooting common errors in file transfers

---

## 🧰 Tools Used
- **Kali Linux (Oracle VM)**
- **Windows VM (Oracle VM)**
- **Apache Web Server**
- **SBD (Secure Backdoor)**
- **Wireshark**

---

## 📋 Steps

### 1️⃣ Start the Apache Web Server
1. Open the terminal on your **Kali Linux** machine.
2. Restart the **Apache Web Server**:
   ```bash
   sudo service apache2 restart
   ```
3. **Ensure both VMs have the correct network settings**:
   - **Adapter 1**: NAT
   - **Adapter 2**: Host-Only
4. **Disable all firewalls and antivirus software** on both machines to avoid interference.

---

### 2️⃣ Download `sbd.exe` to Windows
1. Open **Firefox** on your **Kali Linux** machine.
2. In the browser, type the following URL, replacing `<Kali_IP>` with your Kali machine's IP address:
   ```
   http://<Kali_IP>/sbd.exe
   ```
3. If you get a warning that the file is unsafe:
   - Click **Keep**.
   - Click **Show more**.
   - Click **Keep anyway**.

✅ **The `sbd.exe` file should now be in your Windows Downloads folder.**

---

### 3️⃣ Run SBD on Windows
1. Open **Command Prompt** on your **Windows VM**.
2. Navigate to the **Downloads** directory:
   ```cmd
   cd Downloads
   ```
3. Run the following command to set up **SBD** to listen on port **5555**:
   ```cmd
   sbd -l -p 5555
   ```

✅ **If the command runs successfully, nothing will pop up. This means the listener is running.**

❌ **If you encounter an error like:**
   ```
   The system cannot execute the specified program.
   ```
   - Double-check that all antivirus and firewall protections are **completely disabled**.

---

### 4️⃣ Set Up Wireshark for Capturing
1. On your **Kali Linux** machine, open **Wireshark**.
2. Set the **capture filter** to monitor traffic between the **Kali** and **Windows VMs**:
   ```
   host <Kali_IP> and host <Windows_IP>
   ```
3. Select the correct **interface** (usually **eth1** for Host-Only networks).
   - If the capture filter turns **red**, check that the correct IP addresses are used.
   - Hover over the different interfaces to find the one that turns the capture **green** and use that one.

---

### 5️⃣ Connect to Kali from Windows
1. On your **Kali Linux** terminal, run the following command to connect to the **Windows VM**:
   ```bash
   sbd <Windows_IP> 5555
   ```
2. **To find your Windows IP address**, run the following command in **Command Prompt**:
   ```cmd
   ipconfig
   ```
   - The **Host-Only network IP** will start with **192.168.56.xxx**.

✅ **Once connected, you should see packets appearing in Wireshark.**

---

### 6️⃣ Test the Session
1. On either the **Kali** or **Windows** terminal, type a simple message, such as:
   ```
   hello
   ```
2. The message should appear on the other machine, indicating that the connection is working.

---

### 7️⃣ Stop the Wireshark Capture
1. Go back to **Wireshark** on your **Kali Linux** machine.
2. Stop the capture by pressing **`Ctrl + C`** in the terminal.
3. Save the capture as **sbd-session.pcap** (or any name you prefer).

---

### 8️⃣ Analyze the Wireshark Capture
1. Open the **PCAP file** in **Wireshark**.
2. Review the captured packets.
3. Verify that the **SBD session is encrypted** by default.

---

## 🎯 **Summary**
In this project, a secure connection was established between **Kali Linux** and **Windows** using **SBD**. The connection was captured using **Wireshark**, and the analysis showed that **SBD encrypts sessions by default**, ensuring secure communication between the two machines.


