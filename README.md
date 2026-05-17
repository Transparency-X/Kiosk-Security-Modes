### **What is Kiosk Mode?**
**Kiosk mode** (also called **single-app mode**, **locked-down mode**, or **guided access**) restricts a device to running only a specific app or set of apps, blocking access to other features, settings, or the underlying OS. It’s commonly used in public kiosks, digital signage, or shared devices to prevent misuse, unauthorized access, or tampering.

---

## **Can Kiosk Mode Prevent Spyware/Stalkerware, Screenscraping, or Screen Reading?**

### **✅ What Kiosk Mode *Can* Mitigate**
- **Unauthorized App Installation**: Prevents users from installing spyware/stalkerware if the OS is locked down.
- **Access to System Settings**: Blocks changes to settings that could enable spyware (e.g., accessibility services, admin permissions).
- **Screen Capture/Recording**: On some platforms, kiosk mode can disable screenshots or screen recording.
- **Background Activity**: Limits background processes, reducing the risk of hidden spyware.

### **❌ What Kiosk Mode *Cannot* Fully Prevent**
- **Pre-installed Spyware**: If malware is already on the device (e.g., installed before kiosk mode), it may still run in the background.
- **Kernel-level Spyware**: Advanced spyware (e.g., rootkits) can operate below the OS level and may bypass kiosk restrictions.
- **Physical Access Exploits**: If an attacker has physical access, they may bypass kiosk mode (e.g., via recovery mode, USB debugging, or hardware keyloggers).
- **Screen Scraping via Hardware**: External devices (e.g., HDMI capture cards) can still record the screen.
- **Network-based Attacks**: Kiosk mode doesn’t protect against remote exploits (e.g., phishing, MITM attacks).

---
---

## **How to Set Up Kiosk Mode on Popular OSes**

---

### **🪟 Windows**
#### **1. Assigned Access (Windows 10/11 Pro/Enterprise)**
- **Use Case**: Locks a user account to a single app.
- **Steps**:
  1. Go to **Settings > Accounts > Family & other users**.
  2. Under **Assigned access**, click **Set up assigned access**.
  3. Select a user account and choose the app to allow.
  4. Restart the device to apply.
- **Limitations**:
  - Only works for UWP apps (not all Win32 apps).
  - User can exit with `Ctrl+Alt+Del` unless further restrictions are applied.

#### **2. Windows Kiosk Mode (Enterprise)**
- **Use Case**: Full lockdown for public/enterprise use.
- **Steps**:
  1. Use **Microsoft Intune** or **Group Policy** to configure:
     - `Control Panel > Administrative Templates > System > Custom Logon > Enable assigned access`.
     - Set a **Kiosk account** with restricted permissions.
  2. For **Windows 10/11 Enterprise**, use **Shell Launcher** to replace Explorer with a custom app.
- **Advanced**: Use **Windows Defender Application Control (WDAC)** to block unauthorized apps.

#### **3. Third-Party Tools**
- **KioWare**, **SiteKiosk**, or **Portable Kiosk** for more granular control.

---

### **🍎 macOS**
#### **1. Guided Access (Single-App Mode)**
- **Use Case**: Temporarily locks the Mac to one app.
- **Steps**:
  1. Enable in **System Settings > Accessibility > Guided Access**.
  2. Open the app, then press **⌘ + ⌥ + L** (or triple-click the Touch ID/side button).
  3. Set a passcode and disable hardware buttons if needed.
- **Limitations**:
  - Easy to exit with the passcode.
  - Doesn’t block background processes.

#### **2. Parental Controls (Restricted User)**
- **Use Case**: Create a restricted user account.
- **Steps**:
  1. Go to **System Settings > Users & Groups**.
  2. Create a new **Standard** user and enable **Parental Controls**.
  3. Restrict app access, web browsing, and system changes.
- **Limitations**:
  - User can still install apps if they have the password.

#### **3. Third-Party Tools**
- **Self Service Kiosk** or **Kiosk Pro** for macOS.

---
### **🐧 Linux**
#### **1. Custom Kiosk with X11/Wayland**
- **Use Case**: Run a single app in fullscreen with no window manager.
- **Steps (Ubuntu Example)**:
  1. Install a minimal environment:
     ```bash
     sudo apt install --no-install-recommends xserver-xorg-core xinit openbox
     ```
  2. Create a custom `.xinitrc` file:
     ```bash
     echo "exec /path/to/your/app" > ~/.xinitrc
     ```
  3. Start X with:
     ```bash
     startx
     ```
  4. For autologin, edit `/etc/gdm3/daemon.conf` (or lightdm):
     ```ini
     [daemon]
     AutomaticLoginEnable = true
     AutomaticLogin = kioskuser
     ```
- **Lockdown**:
  - Disable `Ctrl+Alt+F1` (TTY access) by editing `/etc/systemd/logind.conf`:
    ```ini
    NAutoVTs=0
    ReserveVT=0
    ```
  - Remove unnecessary packages (e.g., terminal, file managers).

#### **2. Chrome/Chromium Kiosk Mode**
- **Use Case**: Run Chrome in fullscreen with a single webpage.
- **Steps**:
  1. Launch Chrome with flags:
     ```bash
     chromium-browser --kiosk --noerrdialogs --disable-infobars --disable-session-crashed-bubble https://example.com
     ```
  2. For autostart, add to `~/.config/autostart/`.

#### **3. Tools**
- **Portable Kiosk** (for Linux) or **Matchbox Window Manager** for embedded kiosks.

---
### **🤖 Android**
#### **1. Lock Task Mode (Enterprise)**
- **Use Case**: Locks a device to a single app (or list of apps).
- **Steps**:
  1. **For Work Profile (Android Enterprise)**:
     - Use **Android Management API** or **Intune** to set `lockTaskPackages`.
  2. **For Personal Devices**:
     - Use **Device Owner Mode** (requires factory reset):
       ```bash
       adb shell dpm set-device-owner com.example.kiosk/.DeviceAdminReceiver
       ```
     - Then enable lock task:
       ```bash
       adb shell am start -n com.example.kiosk/.MainActivity --lock-task-mode
       ```
- **Limitations**:
  - Requires **Device Owner** permissions (not possible on non-rooted personal devices).
  - User can exit with a long-press of **Back + Recent Apps** unless disabled.

#### **2. Guided Access (Samsung Knox)**
- **Use Case**: Temporary single-app mode.
- **Steps**:
  1. Enable in **Settings > Accessibility > Guided Access**.
  2. Open the app, then triple-press the **Power button**.
  3. Draw a passcode-protected zone to block touch input.

#### **3. Third-Party Apps**
- **SureLock**, **KioWare for Android**, or **Hexnode UEM**.

---
### **📱 iOS (iPad/iPhone)**
#### **1. Guided Access**
- **Use Case**: Temporary single-app mode with touch/area restrictions.
- **Steps**:
  1. Enable in **Settings > Accessibility > Guided Access**.
  2. Open the app, then triple-press the **Side/Top button** (or Home button on older devices).
  3. Set a passcode and disable hardware buttons/touch areas.
- **Limitations**:
  - Easy to exit with the passcode.
  - Doesn’t block background apps.

#### **2. Single App Mode (Supervised Devices)**
- **Use Case**: Permanent lockdown for enterprise/school devices.
- **Steps**:
  1. Supervise the device using **Apple Configurator 2** or **MDM** (e.g., Jamf, Mosyle).
  2. Push a **Single App Mode** payload to lock the device to one app.
- **Limitations**:
  - Requires **supervision** (not possible on personal devices without wiping).

#### **3. Kiosk Mode via MDM**
- **Use Case**: For managed devices (e.g., retail, education).
- **Steps**:
  - Use an **MDM solution** (e.g., Jamf, Kandji) to:
    - Enable **Single App Mode**.
    - Disable **App Switcher**, **Control Center**, and **Notifications**.
    - Block **Screenshots** and **Screen Recording**.

---
### **📺 ChromeOS**
#### **1. Kiosk Mode**
- **Use Case**: Public displays or single-app devices.
- **Steps**:
  1. Enroll the device in **Chrome Enterprise**.
  2. Set the **Kiosk app** in the **Google Admin Console** under **Device > Kiosk settings**.
  3. Select the app (e.g., Chrome, a web app, or a custom APK).
- **Limitations**:
  - Requires **Enterprise enrollment**.
  - User can exit with `Ctrl+Alt+S` (can be disabled via policy).

---
### **🖥️ Other OSes**
| **OS**               | **Kiosk Mode Method**                          | **Notes**                                  |
|----------------------|-----------------------------------------------|--------------------------------------------|
| **Raspberry Pi OS**  | Autostart a app in `~/.config/lxsession/LXDE-pi/autostart` | Use `xset` to disable input.              |
| **Fire OS**          | **Amazon FreeTime** or **Guided Access**     | Limited to Amazon-approved apps.          |
| **Tizen (Samsung)**  | **Knox Configure** or **Single App Mode**     | Enterprise-only.                          |
| **Fuchsia**          | Not yet widely supported for kiosk use.       | Experimental.                             |

---
---
## **Best Practices to Enhance Security**
1. **Combine with Other Protections**:
   - **Antivirus/Anti-Malware**: Use **Windows Defender**, **Malwarebytes**, or **ClamAV** (Linux).
   - **App Whitelisting**: Only allow known-safe apps (e.g., via **WDAC** on Windows or **Gatekeeper** on macOS).
   - **Disable Debugging**: Turn off **USB debugging** (Android) and **SSH/remote access** (Linux/macOS).

2. **Physical Security**:
   - Use **tamper-proof cases** or **security screws** to prevent hardware access.
   - Disable **USB ports** (via BIOS or software).

3. **Network Security**:
   - Use a **firewall** to block unauthorized connections.
   - Restrict **Wi-Fi/Bluetooth** access in kiosk mode.

4. **Regular Updates**:
   - Keep the OS and kiosk app **fully patched** to prevent exploits.

5. **Monitoring**:
   - Use **SIEM tools** (e.g., Splunk, ELK) or **MDM solutions** to detect anomalies.

---
---
## **Can Kiosk Mode Stop Stalkerware?**
- **Yes, if**:
  - The device is **clean** (no pre-installed spyware).
  - The kiosk mode is **properly configured** (e.g., no background apps, no admin access).
  - The stalkerware requires **user interaction** (e.g., app installation, permissions).
- **No, if**:
  - The spyware is **kernel-level** or **firmware-based**.
  - The attacker has **physical access** to bypass kiosk mode.
  - The spyware uses **zero-day exploits** to escape the sandbox.

---
---
## **Summary Table: Kiosk Mode by OS**

| **OS**       | **Native Kiosk Mode**       | **Third-Party Tools**       | **Spyware Protection** | **Screen Scraping Protection** |
|--------------|-----------------------------|-----------------------------|------------------------|---------------------------------|
| **Windows**  | Assigned Access, Shell Launcher | KioWare, SiteKiosk        | Medium                | Partial (if screenshots disabled) |
| **macOS**    | Guided Access, Parental Controls | Self Service Kiosk      | Low                   | Partial                         |
| **Linux**    | Custom X11/Wayland, Chrome Kiosk | Portable Kiosk          | High (if locked down) | Partial                         |
| **Android**  | Lock Task Mode, Guided Access | SureLock, Hexnode        | Medium                | Partial                         |
| **iOS**      | Guided Access, Single App Mode | MDM solutions            | Medium                | Partial                         |
| **ChromeOS** | Kiosk App (Enterprise)      | -                          | High                  | High                            |

---
---
## **Final Recommendations**
- **For Public Kiosks**: Use **Windows/Linux with Shell Launcher** or **ChromeOS Kiosk Mode** + **MDM**.
- **For Personal Devices**: **Guided Access (iOS/macOS)** or **Lock Task Mode (Android)** + **antivirus**.
- **For Maximum Security**: Combine kiosk mode with **app whitelisting**, **firewall rules**, and **physical security**.
