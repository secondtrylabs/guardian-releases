<p align="center">
  <img src="https://github.com/user-attachments/assets/bc461b7c-2293-4160-94c0-b9ac60c059c3" alt="Guardian" width="420" />
</p>

<p align="center"><b>CPU and GPU Temperature Monitor and Fan Controller for Windows</b></p>

Guardian keeps your CPU and GPU temperatures in the system tray where you can always see them, and opens into a dashboard with live gauges, history charts, every fan in your system, and fan control based on CPU or GPU temperature. If something goes wrong, such as a chip running hot or a fan or pump stopping, Guardian sounds an alarm until you deal with it.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e003983f-ad22-413b-b47d-a9c03876d3c8" alt="Guardian dashboard" width="760" />
</p>

Developed by **SecondTry Labs**

**[Download the latest release](https://github.com/secondtrylabs/guardian-releases/releases/latest)**

---

## Table of Contents

- [Installation](#installation)
- [Tray Temperatures](#tray-temperatures)
- [Desktop Overlay](#desktop-overlay)
- [Dashboard](#dashboard)
- [Cooling and Fan Control](#cooling-and-fan-control)
- [Alarms](#alarms)
- [Sensor List](#sensor-list)
- [Options](#options)
- [Updates](#updates)
- [FAQ](#faq)
- [Credits](#credits)

---

## Installation

1. Download `Guardian-Setup-x.x.x.exe` from the [Releases](https://github.com/secondtrylabs/guardian-releases/releases) page.
2. Run the installer. It installs to `C:\Program Files\Guardian` and adds Start Menu and desktop shortcuts.
3. Leave **Start Guardian** ticked on the last page.

**System requirements**
- Windows 10 or 11, 64-bit
- Administrator rights. Guardian reads CPU temperatures and controls fans through a hardware driver, which Windows only allows for administrators.
- The **PawnIO** driver for CPU temperatures and motherboard fans. It's included: the installer offers to install it if it's missing, and updates an older version automatically. Without it, GPU readings still work.
- Built and tested on an AMD Ryzen CPU with an NVIDIA GeForce GPU.

> **Note:** The installer isn't code-signed yet, so Windows SmartScreen may show "Windows protected your PC". Click **More info**, then **Run anyway**.

---

## Tray Temperatures

<img src="https://github.com/user-attachments/assets/cc04452b-6cf8-4304-b908-61be44b9541c" alt="CPU and GPU temperatures in the system tray" width="80" />

Guardian puts two live temperatures next to the clock:
- **Orange strip:** CPU temperature
- **Green strip:** GPU temperature

The numbers turn **amber** when a chip gets warm and **red** when it reaches its Hot threshold. Hover for details, click either one to open Guardian, and right-click for **Open Guardian** and **Exit**.

> **Tip:** Windows hides new tray icons at first. Click the **^** next to the clock and drag both temperatures onto the taskbar to keep them visible.

---

## Desktop Overlay

A small always-on-top CPU and GPU panel you can park anywhere, including right on the taskbar of a second monitor, so you can watch temperatures while gaming. Game windows hide the tray, but not a second screen.

<img src="https://github.com/user-attachments/assets/633bf270-bf68-4b7d-9e57-20a9a680bb8f" alt="Locked overlay blending into the taskbar" width="363" />

Turn it on in **Options → General → Display → Desktop Overlay**. It shows each chip's **temperature**, **load** and **power**, and the temperatures turn **amber** when warm and **red** at the Hot threshold.

**Placing it**

<img src="https://github.com/user-attachments/assets/acb42534-ea11-418c-b3ae-288c50923394" alt="Unlocked overlay with the Guardian shield, ready to drag" width="395" />

- While **unlocked**, the overlay shows a card and the Guardian shield so it's easy to find. Drag it wherever you want it.
- Then **lock** it with **Lock Overlay Position** in Options, or by right-clicking it and choosing **Lock Position**. Once locked it blends into the taskbar, and matches a light or dark taskbar automatically.
- Clicking a locked overlay opens Guardian. While unlocked, double-click opens it.
- It remembers where you left it, and stays anchored by its right edge, so changing numbers never push it into the clock.

**Right-click** it for **Open Guardian**, **Silence Alarm** (while an alarm is ringing), **Lock Position** or **Unlock Position**, **Hide Overlay** and **Exit Guardian**. While an alarm is ringing, its border pulses red.

> **Tip:** Using the overlay instead of the tray? Turn off **Tray Temperatures** in Options. Guardian then keeps a single icon in the tray for its menu and alarm notifications.

---

## Dashboard

The CPU and GPU cards each show:
- A **gauge** with the current temperature, plus tick marks at the Warm and Hot thresholds
- A **NORMAL / WARM / HOT** status
- **Load, power, clock speed**, and a second temperature (CCD for the CPU, hot spot for the GPU)
- A **two minute history chart**
- Detail rows such as average and effective clocks, memory junction temperature, core voltage and VRAM use

**Core → hot spot gap** (GPU card) is the difference between the GPU's core and hottest point. On liquid-cooled cards, including those with a built-in AIO, a pump that's struggling makes this gap widen quickly under load, so it's a good early warning.

---

## Cooling and Fan Control

The **Cooling** card lists every fan Guardian can see, on the graphics card and on motherboard headers, with live RPM. Fans on a curve following the CPU have an **orange** strip, and fans on the graphics card or following the GPU have a **green** one. Empty motherboard headers are hidden until you click **Show all fans**.

Click any fan to open its settings:

<p align="center">
  <img src="https://github.com/user-attachments/assets/ba84787e-ea62-4e62-ba6d-7d1c4d570932" alt="Fan settings with a temperature curve" width="480" />
</p>

- **Name it**, for example "Front intake" or "Radiator".
- **Mark it as a pump.** Pumps never run below 50%.
- **Hide it** from the dashboard.
- **Control:**
  - **Auto (BIOS / Driver):** Guardian leaves the fan alone. This is the default.
  - **Fixed Speed:** runs at the percentage you choose.
  - **Temperature Curve:** follows the **CPU** or **GPU** temperature. Drag points to shape the curve, double-click to add a point, right-click to remove one, or start from the **Silent**, **Balanced** or **Performance** presets. A live marker shows where the current temperature sits.

Fans on the graphics card always follow the GPU. Motherboard fans can follow either, which is handy for GPU radiator fans plugged into the motherboard.

**Safety**
- Curves speed fans up quickly and slow them down gently, so they don't rev up and down with every brief temperature change.
- If the CPU reaches 88°C, the GPU 85°C, or the GPU hot spot 100°C, every fan Guardian controls goes to 100%.
- If a curve's temperature reading is lost, that fan goes to 100%.
- When you exit Guardian, or if a sensor error occurs, every fan goes back to BIOS or driver control.

> **Using FanControl or another fan tool?** Don't let two apps control the same fan. Remove it from the other tool first. Guardian warns you if FanControl is running.

---

## Alarms

Guardian's alarm means something needs your attention. It goes off when:
- The **CPU** reaches its Hot threshold (85°C by default)
- The **GPU** reaches its Hot threshold (83°C by default)
- A **fan or pump stops**: a fan Guardian is controlling, or anything you've marked as a pump, reads 0 RPM for 5 seconds

When it goes off:
- The alarm sound plays and **repeats every 30 seconds** until the problem clears or you silence it.
- A **red banner** appears at the top of Guardian with a **Silence** button.
- A **Windows notification** appears. Clicking it opens Guardian.
- **Silence Alarm** appears in the tray menu.

Silence stops the sound for the current problem only. The banner stays until the problem clears, and any new problem sounds the alarm again.

---

## Sensor List

Click the **waveform icon** in the header to open the Sensor List beside the dashboard. It shows every sensor Guardian can read (temperatures, fans, clocks, voltages, power, loads and more), grouped by device and updating live. **Copy All** copies the whole list as text, which is useful for troubleshooting.

<p align="center">
  <img src="https://github.com/user-attachments/assets/367b7955-af62-4728-b55c-f890c846b826" alt="Sensor List next to the dashboard" width="760" />
</p>

---

## Options

Click the **gear icon** in the header.

**General**
- **Start with Windows:** starts Guardian when you sign in, with no UAC prompt.
- **Start Minimized:** goes straight to the tray at sign-in.
- **Minimize to Tray:** minimizing hides Guardian to the tray instead of the taskbar.

**Alerts**
- Choose the alarm sound and **Preview** it, then set the volume.
- **Edit** the CPU and GPU Hot thresholds. These also set the gauge colors, the status labels and the tray-icon colors.
- Turn each alarm trigger on or off.

<p align="center">
  <img src="https://github.com/user-attachments/assets/35cb75c9-517d-4101-a1b6-33a19fba0079" alt="Options, Alerts tab" width="560" />
</p>

**About**
- Version, change log, credits, and **Check for Updates**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/71cfeb58-16d1-4476-be81-d8c55e055d35" alt="Options, About tab" width="560" />
</p>

---

## Updates

Guardian checks this page for new releases shortly after it starts and then twice a day. When an update is available, an **Update** button appears in the header. You can also check any time from **Options → About → Check for Updates**.

**Download and Install** downloads the new installer and runs it. Guardian closes itself first and hands your fans back to the BIOS. Your settings, fan names and curves are kept.

Guardian only asks GitHub for the latest version number. No data about your PC is collected or sent.

---

## FAQ

### Why does Guardian need administrator rights?
CPU temperatures and motherboard fans are read through the PawnIO hardware driver, and Windows only lets administrators use it. **Start with Windows** uses a scheduled task, so you don't get a UAC prompt at every sign-in.

### My CPU temperature shows "--"
The PawnIO driver isn't installed. Restart Guardian and accept the offer to install it, or install it from [pawnio.eu](https://pawnio.eu/).

### A fan won't go to 0% or stops responding
Many fans have a minimum speed, and graphics card drivers often won't go below about 30%. Only the card's own idle mode, on Auto, can fully stop GPU fans. Motherboard fans may also depend on the header being set to PWM or DC mode in your BIOS.

### Can I use Guardian with FanControl?
Yes, as long as the two apps don't control the same fan. Guardian only takes control of fans you set to Fixed Speed or a Temperature Curve.

### Guardian was force-closed and a fan is stuck at one speed
If Guardian is killed (for example from Task Manager), it can't hand fans back first. Start Guardian again, or restart your PC, and the fans return to normal control.

### Where is my data stored?

| Data | Location |
|------|----------|
| Settings, fan names and curves | `%LOCALAPPDATA%\Guardian\settings.json` |
| Log | `%LOCALAPPDATA%\Guardian\guardian.log` |
| Application | `C:\Program Files\Guardian\` |

Uninstalling (Settings → Apps) removes the application and the Start with Windows task, and keeps your settings.

---

## Credits

**Alarm sounds** from [Freesound](https://freesound.org/):
- "1 alarm short e" and "3 alarm short e" by jobro (CC BY 3.0)
- "Beep beep beep beep beep beep" by AceOfSpadesProduc100 (CC BY 4.0)
- "alarm.wav" by coltonmanz (CC BY 4.0)
- "two_tone_alarm_repeating" by theprinternet (CC0)

**Hardware access:** [LibreHardwareMonitor](https://github.com/LibreHardwareMonitor/LibreHardwareMonitor) (MPL 2.0) and the [PawnIO](https://pawnio.eu/) driver by namazso.

---

*© 2026 SecondTry Labs. All rights reserved.*
