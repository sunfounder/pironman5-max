.. note::

    Hello, welcome to the SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasts Community on Facebook! Dive deeper into Raspberry Pi, Arduino, and ESP32 with fellow enthusiasts.

    **Why Join?**

    - **Expert Support**: Solve post-sale issues and technical challenges with help from our community and team.
    - **Learn & Share**: Exchange tips and tutorials to enhance your skills.
    - **Exclusive Previews**: Get early access to new product announcements and sneak peeks.
    - **Special Discounts**: Enjoy exclusive discounts on our newest products.
    - **Festive Promotions and Giveaways**: Take part in giveaways and holiday promotions.

    👉 Ready to explore and create with us? Click [|link_sf_facebook|] and join today!

.. _nas_view_control_commands:

Control with Commands
========================================
In addition to viewing data from the Pironman 5 and controlling various devices through the Dashboard, you can also use commands to control them.

.. note::

  * For the **Home Assistant** system, you can only monitor and control the Pironman 5 through the dashboard by opening the webpage at ``http://<ip>:34001``.
  
  .. * For the **Batocera.linux** system, you can only monitor and control the Pironman 5 via commands. It is important to note that any changes to the configuration require a restart of the service using ``pironman5 restart`` to take effect.

View the Basic Configurations
-----------------------------------

The ``pironman5`` module offers basic configurations for Pironman, which you can review with the following command.

.. code-block:: shell

  sudo pironman5 -c

.. The standard configurations appear as follows:

.. .. code-block:: 

..   {
..       "auto": {
..           "rgb_color": "#0a1aff",
..           "rgb_brightness": 50,
..           "rgb_style": "breathing",
..           "rgb_speed": 50,
..           "rgb_enable": true,
..           "rgb_led_count": 4,
..           "temperature_unit": "C",
..           "gpio_fan_mode": 2,
..           "gpio_fan_pin": 6
..       }
..   }

.. Customize these configurations to fit your needs.

Use ``pironman5`` or ``pironman5 -h`` for instructions.

.. code-block::

  Pironman 5 NAS command line interface

  positional arguments:
    {start,restart,stop}  Command

  options:
    -h, --help            show this help message and exit
    -v, --version         Show version
    -c, --config          Show config
    -dl {debug,info,warning,error,critical}, --debug-level {debug,info,warning,error,critical}
                          Debug level
    --background [BACKGROUND]
                          Run in background
    -rd, --remove-dashboard
                          Remove dashboard
    -cp [CONFIG_PATH], --config-path [CONFIG_PATH]
                          Config path
    -eh [ENABLE_HISTORY], --enable-history [ENABLE_HISTORY]
                          Enable history, True/true/on/On/1 or False/false/off/Off/0
    -u [{C,F}], --temperature-unit [{C,F}]
                          Temperature unit
    -oe [OLED_ENABLE], --oled-enable [OLED_ENABLE]
                          OLED enable True/true/on/On/1 or False/false/off/Off/0
    -or [{0,180}], --oled-rotation [{0,180}]
                          Set to rotate OLED display, 0, 180
    -os [OLED_SLEEP_TIMEOUT], --oled-sleep-timeout [OLED_SLEEP_TIMEOUT]
                          OLED sleep timeout in seconds



.. note::

  Each time you modify the status of ``pironman5.service``, you need to use the following command to make the configuration changes take effect.

  .. code-block:: shell

    sudo systemctl restart pironman5.service


* Verify the ``pironman5`` program status using the ``systemctl`` tool.

  .. code-block:: shell

    sudo systemctl status pironman5.service

* Alternatively, inspect the program-generated log files.

  .. code-block:: shell

    ls /var/log/pironman5/



Check the OLED Screen
-----------------------------------

When you have installed the ``pironman5`` library, the OLED screen displays CPU, RAM, Disk Usage, CPU Temperature, and the Raspberry Pi's IP Address, and it shows this every time you reboot.

If your OLED screen does not display any content, you need to first check if the OLED's FPC cable is connected properly.

Then you can check the program log to see what might be the problem through the following command.

.. code-block:: shell

  cat /var/log/pironman5/pm_auto.oled.log

Or check if the OLED's i2c address 0x3C is recognized:

.. code-block:: shell

  i2cdetect -y 1


Setting the OLED
-----------------------------------


When the OLED is installed and rebooted, it will light up.

You can turn on/off the OLED using the following command. The argument could be ``on`` or ``off``.

  .. code-block:: shell
    
    sudo pironman5 -oe on


You can set the rotation of the OLED using the following command. The argument could be ``0`` or ``180``.

  .. code-block:: shell

    sudo pironman5 -or 180

To protect the OLED, the OLED will be turned off. After the OLED is turned off, you can click the power button to wake up the OLED. After a certain time, the OLED will be turned off again. You can use the following command to adjust the OLED's sleep time. The range is (5s to 600s). The following command sets the OLED's sleep time to 10s.

  .. code-block:: shell
    
    sudo pironman5 -os 10
  


