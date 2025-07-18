.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

.. _install_os_sd_rpi:

Installing the OS on a Micro SD Card
============================================================
If you are using a Micro SD card, you can follow the tutorial below to install the system onto your Micro SD card.

.. .. raw:: html

..     <iframe width="700" height="500" src="https://www.youtube.com/embed/-5rTwJ0oMVM?start=343&end=414&si=je5SaLccHzjjEhuD" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

**Required Components**

* A Personal Computer
* A Micro SD card and Reader

**Steps**

#. Insert your SD card into your computer or laptop using a Reader.

#. Within the |link_rpi_imager|, click **Raspberry Pi Device** and select the **Raspberry Pi 5** model from the dropdown list.

   .. image:: img/os_choose_device_pi5.png
      :width: 90%

#. Select **Operating System** and opt for the recommended operating system version.

   .. image:: img/os_choose_os.png
      :width: 90%

#. Since OpenMediaVault only supports a non-desktop version of the system, choose the **Raspberry Pi OS Lite** version.

   .. image:: ../img/omv/omv-install-1.png
      :width: 90%



#. Click **Choose Storage** and select the appropriate storage device for the installation.

   .. image:: img/os_choose_sd.png
      :width: 90%

#. Click **NEXT** and then **EDIT SETTINGS** to tailor your OS settings. 

   .. image:: img/os_enter_setting.png
      :width: 90%
      

   * Define a **hostname** for your Raspberry Pi. The hostname is your Raspberry Pi's network identifier. You can access your Pi using ``<hostname>.local`` or ``<hostname>.lan``.

     .. image:: img/os_set_hostname.png
   

   * Create a **Username** and **Password** for the Raspberry Pi's administrator account. Establishing a unique username and password is vital for securing your Raspberry Pi, which lacks a default password.

     .. image:: img/os_set_username.png      

   * Configure the wireless LAN by providing your network's **SSID** and **Password**.

     .. note::

       Set the ``Wireless LAN country`` to the two-letter `ISO/IEC alpha2 code <https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements>`_ corresponding to your location.

     .. image:: img/os_set_wifi.png


   * To remotely connect to your Raspberry Pi, enable SSH in the Services tab.

     * For **password authentication**, use the username and password from the General tab.
     * For public-key authentication, choose "Allow public-key authentication only". If you have an RSA key, it will be used. If not, click "Run SSH-keygen" to generate a new key pair.

     .. image:: img/os_enable_ssh.png

   * The **Options** menu lets you configure Imager's behavior during a write, including playing sound when finished, ejecting media when finished, and enabling telemetry.

     .. image:: img/os_options.png

#. When you've finished entering OS customisation settings, click **Save** to save your customisation. Then, click **Yes** to apply them when writing the image.

   .. image:: img/os_click_yes.png
      :width: 90%
      

#. If the SD card contains existing data, ensure you back it up to prevent data loss. Proceed by clicking **Yes** if no backup is needed.

   .. image:: img/os_continue.png
      :width: 90%
      

#. When you see the "Write Successful" popup, your image has been completely written and verified. You're now ready to boot a Raspberry Pi from the Micro SD Card!

   .. image:: img/os_finish.png
      :width: 90%
      