.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

.. _nas_set_up_pironman5:

5. Set up or Install Software
================================================

Now that the system has been written to either the Micro SD or NVMe SSD, you can insert them into the Pironman 5 slot. Then press the power button to turn on the device.

After powering on, you will see the various power LEDs lit up, but the OLED screen, RGB LEDs, and RGB fans (the two fans on the side) will not be operational yet, as they need to be configured. If there is a screen garbling issue, please ignore it for now; it will be resolved after configuration.

Before configuring, you need to boot up and log into your Raspberry Pi. If you're unsure how to log in, you can visit the official Raspberry Pi website: |link_rpi_get_start|.

You can then proceed to select the configuration tutorial based on your system.


.. toctree::
    :maxdepth: 1

    set_up_rpi_os 


.. set_up_home_assistant

.. set_up_batocera



**Button Functions**

* **Short press**: Powers on the Raspberry Pi, wakes up the OLED screen, or cycles through different OLED display modes.
* **Long press (2 seconds)**: Initiates a safe shutdown of the Raspberry Pi.
* **Long press (5 seconds)**: Forces an immediate power cut (hard shutdown).

.. note:: The 5-second long press is equivalent to unplugging the power and should only be used when the system is unresponsive, as it may lead to data loss or file system corruption.