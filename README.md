
# **DaVinci Resolve on Lutris** 🐧

<img src="./Assets/DaVinci_Resolve_Studio.png" width="200" alt="DaVinci Resolve on Linux Logo">

### Before doing anything, make sure you have a `.exe` version of DaVinci Resolve apps. You can download DaVinci Resolve from the official Blackmagicdesign websites
 - [Download DaVinci Resolve 20](https://www.blackmagicdesign.com/products/davinciresolve)

*A curated repository documenting how to run **DaVinci Resolve (Windows builds)** on **GNU/Linux** using **WINE-based compatibility layers**.*

This project focuses on **real-world, reproducible setups** using **Lutris**, **Wine**, and **Proton**, including **custom Wine forks** with **DirectML**, **OpenCL**, and **CUDA** support where available.

---

## ⚠️ Before You Start

### **Required**

* A modern **Linux desktop** (x86_64 recommended)
* **Lutris**
* A **Wine or Proton runner** available inside Lutris
* **winetricks**
* **Windows installer** (`.exe`) for:

  * **DaVinci Resolve**
* **DirectML Redistributable** → `directml.dll` (**mandatory**)

### **Optional / Hardware-Dependent**

* `opencl.dll` — OpenCL acceleration (may be requested at runtime)
* `nvcuda.dll` — NVIDIA CUDA support (**x86_64 only**)

> ℹ️ **Important Note**
> The Linux-native version of DaVinci Resolve **does not support H.264/H.265 decoding** unless using the Studio edition and has **GPU limitations** depending on vendor and driver stack.
> Running the **Windows build under Wine** bypasses many of these restrictions.

---

## 🚀 Quick Start (Simple Path)

This guide assumes **basic Linux familiarity** and prioritizes **minimum friction** over experimentation.

---

## **1. Install winetricks**

`winetricks` is used to install missing Windows runtime components inside Wine prefixes.

### Debian / Ubuntu

```bash
sudo apt install winetricks
```

### Fedora

```bash
sudo dnf install winetricks
```

### Arch Linux

```bash
sudo pacman -Sy winetricks
```

Repository:
👉 [https://github.com/Winetricks/winetricks](https://github.com/Winetricks/winetricks)

---

## **2. Install Lutris**

### Recommended

* **Flatpak (preferred)**
  👉 [https://flathub.org/apps/net.lutris.Lutris](https://flathub.org/apps/net.lutris.Lutris)

### Alternatives

* Official packages:
  👉 [https://github.com/lutris/lutris/releases](https://github.com/lutris/lutris/releases)

---

## **3. Download DaVinci Resolve on Linux Toolkit**

This repository provides a **preconfigured toolkit** containing:

* Custom Wine runners
* Required DLL overrides
* Helper scripts for Lutris

### Steps

1. Download
   👉 **DaVinci-Resolve-on-Linux.tar.gz**
   [https://github.com/AnujaGajaweera/DaVinci-Resolve-on-Linux/releases](https://github.com/AnujaGajaweera/DaVinci-Resolve-on-Linux/releases)
2. Extract the archive
3. You should now have:

   ```text
   DaVinci-Resolve-on-Linux/
   ```

You will register this runner and configuration in Lutris later.

---

## **4. Install DirectML**

**DirectML is mandatory** for GPU-accelerated rendering and inference.

### **Method A – Official Redistributable**

1. Download the **DirectML `.nupkg`**
2. Rename it to `.zip`
3. Extract the archive
4. Locate:

   ```text
   bin/<architecture>/DirectML.dll
   ```

---

>  [!NOTE] 
> **Pre-Extracted version (Unofficial)**
> * You can download `directml.dll` from:
  👉 [https://github.com/AnujaGajaweera/Linux-DaVinci-Resolve-Guide/DirectML/directml.dll](https://github.com/AnujaGajaweera/Linux-DaVinci-Resolve-Guide/blob/main/DirectML/directml.dll)
 ⚠️ Unofficial binaries are provided for convenience only.

---

## **5. Optional GPU Libraries**

You may be prompted for these at runtime:

* **OpenCL acceleration**
  👉 `opencl.dll`
  [https://www.dll-files.com/opencl.dll.html](https://www.dll-files.com/opencl.dll.html)

* **NVIDIA CUDA (x86_64 only)**
  👉 `nvcuda.dll`
  [https://www.dll-files.com/nvcuda.dll.html](https://www.dll-files.com/nvcuda.dll.html)
  Nvidia drivers are **not strictly required**, but significantly improve **performance, stability, and feature compatibility**.

---

## **6. Generate the Lutris Installer**

You can automatically generate a **ready-to-import Lutris installer**:

```bash
python3 resolve_lutris_installer.py \
  --action generate \
  --runner wine \
  --target all \
  --output-dir .
```

This produces a `.yml` installer compatible with Lutris.

### 💡 Alternatively, download a **pre-generated installer** from the Releases section:
[https://github.com/AnujaGajaweera/DaVinci-Resolve-on-Linux/blob/main/davinci-resolve.yml](https://github.com/AnujaGajaweera/DaVinci-Resolve-on-Linux/blob/main/davinci-resolve.yml)

---

## 🧪 Status

* ✅ DaVinci Resolve (Windows build): **Working**
* ✅ H.264 / H.265 decoding: **Enabled**
* ⚠️ Performance varies by GPU, driver, and Wine runner
