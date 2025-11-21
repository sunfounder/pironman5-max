.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!


FAQ
=============================

This section provides answers to the most common issues and questions when installing,
configuring, and operating the Pironman 5 NAS. The content is organized by topic for clarity.

.. contents::
   :local:
   :depth: 2

General Questions
-----------------------------

**What operating systems are supported for Pironman 5 NAS?**  
Pironman 5 NAS officially supports Raspberry Pi OS Lite (64-bit).  
Desktop versions and Home Assistant OS are **not** supported for OpenMediaVault installation.

**Can I boot directly from NVMe SSD?**  
Yes. The Raspberry Pi 5 can boot from NVMe after updating the bootloader and setting the
boot priority to *NVMe/USB → SD Card*. Ensure you complete the bootloader update steps
before writing the OS to the NVMe drive.

**Do both NVMe slots support booting?**  
Yes. Both M.2 NVMe slots support booting, but only PCIe Gen2 speeds are supported due to
the PCIe switch.

Hardware & Compatibility
------------------------

**Which NVMe SSDs are compatible?**  
Most 2280 PCIe Gen3/Gen4 drives are compatible but will operate at PCIe Gen2 speed.
A compatibility list is available in the hardware chapter.

**Can I use 3.5'' HDDs without external power?**  
Yes. The NAS HAT provides 12V power via the included power supply (12V/5A).  
Do not use lower-current adapters.

**Why is the OLED screen blank?**  
Common causes:

1. The FPC cable is not fully inserted.  
2. The pironman5 service is not running.  
3. The I2C interface is disabled.  
4. The OLED address (0x3C) is not detected.

Check with:

.. code-block:: bash

    i2cdetect -y 1

If 0x3C is missing, recheck the cable.

Cooling & Fans
--------------

**Why is the top fan not spinning?**  
Check the following:

- The fan is connected to the correct header.
- The pironman5 service is running.
- The fan mode is not set to "off" in the dashboard.
- The jumper on the Fan Frequency Generator is set correctly.

**The fan speed reading is always 0 RPM. What should I do?**

- Ensure the fan supports tachometer output.
- Verify the tachometer jumper is connected to the correct fan (TOP FAN or CPU FAN).
- Restart the service:

.. code-block:: bash

    sudo systemctl restart pironman5.service

Power & Button
--------------

**The system does not turn on automatically. How do I enable auto-power?**  
Move the ON/OFF jumper on the NAS HAT to the **ON** position.  
This enables auto-power-on when the 12V adapter is connected.

**Long-press shutdown does not fully power off. Why?**  
You must enable:

.. code-block:: 
   
   POWER_OFF_ON_HALT=1



Using:

.. code-block:: bash

    sudo rpi-eeprom-config -e

Without this setting, the microcontroller cannot cut main power after the OS halts.

Storage & RAID
--------------

**Why doesn’t OpenMediaVault detect my NVMe or SATA drives?**

- Confirm the OS is Raspberry Pi OS Lite (desktop version will fail).
- Ensure the PCIe boot delay was disabled by adding:

  ``dtparam=pciex1_no_10s=on``

  to ``config.txt`` on the boot partition.
- Check cable seating for SATA drives.
- Reboot the system after installing OMV.

**Creating RAID 0/1 fails with "500 Internal Server Error". What should I do?**  
This is a known OMV issue. Reboot OMV and try again.  
Ensure both drives are wiped before creating RAID.

**Why is RAID synchronization extremely slow?**  
RAID operations are CPU-bound on Raspberry Pi.  
Speed improves after initial sync completes. You can monitor progress in OMV under
*Storage → RAID Management*.

OpenMediaVault
--------------

**I cannot access OMV using http://raspberrypi.local. What should I try?**

- Use the IP address instead: ``http://<Pi-IP>``  
- Ensure both your computer and the Pi are on the same network.
- If using Wi-Fi, confirm the SSID and country code are set in Raspberry Pi Imager.
- If you enabled SSH key-only login, ensure the key is valid.

**OMV asks for login but credentials do not work. What is the default?**

- **Username:** ``admin``
- **Password:** ``openmediavault``

If you changed it and forgot, reset via SSH:

.. code-block:: bash

    sudo omv-rpc -u admin "UserMgmt" "setPassword" '{"username":"admin","password":"newpass"}'

Dashboard & pironman5 Module
-----------------------------

**The dashboard at http://<ip>:34001 does not load. How can I fix it?**

1. Verify the service is running:

.. code-block:: bash

    sudo systemctl status pironman5.service

2. Restart the service:

.. code-block:: bash

    sudo systemctl restart pironman5.service

3. Ensure port 34001 is not blocked by iptables or firewall rules.

**How do I clear dashboard historical data?**  
Open the Settings menu in the top-right corner and click **CLEAR**.

NVMe Boot Issues
----------------

**My Pi boots only when an SD card is inserted, even after installing the OS on NVMe.**  
Possible fixes:

- Ensure the bootloader was correctly written using "NVMe/USB Boot".
- Ensure ``config.txt`` contains:

  ``dtparam=pciex1_no_10s=on``

- Reflash the NVMe OS image.
- Disconnect all USB storage devices during testing.

**The NVMe drive is not detected at all. What can I do?**

- Reseat the NVMe module.
- Try the other NVMe slot.
- Ensure the drive is single-sided (double-sided drives may touch the metal case).
- Some high-power Gen4 SSDs may fail; try a lower-power model.

Network
-------

**The 2.5G Ethernet port doesn't show up. What should I check?**

- Kernel 6.1+ includes r8169 driver required for RTL8125.
- Check with:

.. code-block:: bash

    ip link

If not present:

- Update Raspberry Pi OS:  

.. code-block:: bash

    sudo apt update && sudo apt full-upgrade

**Can I use both Gigabit Ethernet and 2.5G Ethernet simultaneously?**  
Yes. Both interfaces operate independently and can be bonded or bridged using Linux tools.

Troubleshooting Summary
-----------------------

**Where can I find logs if something goes wrong?**

Pironman service logs:

.. code-block:: bash

    ls /var/log/pironman5/

Check OLED logs:

.. code-block:: bash

    cat /var/log/pironman5/pm_auto.oled.log

Check service status:

.. code-block:: bash

    sudo systemctl status pironman5.service

**What should I try first if “something doesn't work”?**

A recommended quick checklist:

1. Reboot the Pi.  
2. Check power supply (12V/5A).  
3. Confirm cables (NVMe, SATA, OLED).  
4. Update the system.

.. code-block:: bash

    sudo apt update && sudo apt full-upgrade

5. Restart pironman5:

.. code-block:: bash

    sudo systemctl restart pironman5.service

