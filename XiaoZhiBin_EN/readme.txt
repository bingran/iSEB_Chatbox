XiaoZhi Device Setup Guide
==========================

This guide explains how to set up a XiaoZhi device using ESP-IDF v5.4.1 and flash the firmware.

Requirements
------------
- Windows PC
- USB cable to connect the XiaoZhi device
- ESP-IDF v5.4.1 installer
- Firmware files:
    - bootloader.bin
    - partition-table.bin
    - ota_data_initial.bin
    - xiaozhi.bin
    - generated_assets.bin

Steps
-----

1. Install ESP-IDF v5.4.1
   -----------------------
   1. Download the ESP-IDF v5.4.1 Windows Offline Installer from Espressif.
   2. Run the installer and select the installation folder, e.g., C:\ESP\v5.4.1\esp-idf
   3. Allow the installer to set up Python, Git, CMake, and the toolchain.
   4. Installation complete. ESP-IDF is ready to use.

2. Prepare Command Prompt
   -----------------------
   1. Open Command Prompt.
   2. Navigate to the ESP-IDF folder:
      
      cd C:\ESP\v5.4.1\esp-idf

   3. Set up environment variables for the session:

      call export.bat

   Note: Run `export.bat` in each new CMD session before using ESP-IDF tools.

3. Flash XiaoZhi Firmware
   ------------------------
   1. Connect the XiaoZhi device via USB.
   2. Flash the firmware (replace COM13 with your device's COM port if needed):

      call esptool.py -p COM13 -b 460800 write_flash --flash_mode dio --flash_size 16MB --flash_freq 80m ^
      0x0 bootloader.bin ^
      0x8000 partition-table.bin ^
      0xD000 ota_data_initial.bin ^
      0x20000 xiaozhi.bin ^
      0x800000 generated_assets.bin

4. Configure Network
   ------------------
   1. Power on the XiaoZhi device.
   2. Connect to the XiaoZhi Wi-Fi network from your PC or mobile device.
   3. Update the device’s internet credentials (Wi-Fi SSID & password).

5. Register and Set Up Device
   ----------------------------
   1. Follow the online guide: https://ai.feishu.cn/wiki/JiQowaSe1itt07kyVvZcHFcQnee
   2. Complete device registration and setup.
   3. Verify that the device is connected to the internet.

Tips
----
- Always run `export.bat` before flashing or using ESP-IDF commands.
- Confirm the correct COM port in Windows Device Manager before flashing.
- Keep all firmware files in the same folder for simplicity.
- The flashing command assumes a 16 MB flash; adjust if needed.
