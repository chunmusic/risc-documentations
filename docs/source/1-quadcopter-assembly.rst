Quadcopter Assembly
=====

Basic principles
-----

Feel free to place the components anywhere on the frame but take care of wires. Refer to quadcopters we already have in the lab. Carefully choose zipties, shrinking tubes, double sided tapes or soldering for different situations. Generally, for fixing motor wires we use zipties. Shrinking tubes are for permanent connection between wires when soldering.

Preliminaries
------

This tutorial assumes you have the following skills:

* :doc:`1-ros-basics`.

* Soldering, if not, please refer to basic skill `video <https://youtu.be/Qps9woUGkvI>`_.


* Basic knowledge about LiPo batteries. Answer the following questions. You may read `this article <https://rogershobbycenter.com/lipoguide/>`_. 

  - What do 3s, 4s mean?
  - What does 20c mean?
  - What does 1400mAh mean?
  - What are the parameters of your battery?
  - How to charge LiPo battery? How to measure it voltage using battery meter?
  - What’s the minimum voltage to use a LiPo on the quadcopter?

* Basic knowledge about motors. Answer the following questions. You may refer to `this article <https://www.dronetrest.com/t/brushless-motors-how-they-work-and-what-the-numbers-mean/564>`_.

  + Different types of motors. We are using brushless motor for quadcopters.
  + What does KV2200 means? What will be changed if KV number grows?
  + What are the parameters of your motors?

.. danger:: Do not leave your battery plugged in your quadcopter for a long time and never discharge a LiPo battery below 3.4V per cell.

Hardware assembly
-----

Introduction
^^^^^

You will need

* Quadcopter frame. Frames 250 or 330 will be a good start. The value 250/330 means the motor to motor diameter, as shown below.

.. image:: ../_static/quad-diam.png
   :scale: 50 %
   :align: center


* Power distribution board to distribute power from a battery to 4 ESCs (no need in case of F330 and F450).


.. image:: ../_static/distro-power.jpg
   :scale: 50 %
   :align: center


* Flight Controller. Use any flight controller available in the lab. Just make sure you have compatible power modules, receivers, GPS, and other additional modules. The documentations for each board are available `here <https://docs.px4.io/en/flight_controller/pixhawk_series.html>`_.

* Brushless motors and propellers. For mini quad pilots, 3-blade (or tri-blade) propellers are equally popular as the two blades, they are commonly used in both racing and free-style flying. Some people prefer tri-blades because it has more grip in the air. Basically, by adding more blade it’s effectively adding more surface area, and therefore it generates more thrust in the expense of higher current draw and more drag. 

.. note:: 
  
  There are 2 types of format that manufacturers use.

  L x P x B or LLPP x B where L- length, P – pitch, B – number of blades.

  For example 6×4.5 (also known as 6045) propellers are 6 inch long and has a pitch of 4.5 inch. Another example, 5x4x3 (sometimes 5040×3) is a 3-blade 5″ propeller that has a pitch of 4 inch. “BN” indicates Bullnose props.

  Sometimes you might see **R** or **C** after the size numbers, such as 5x3R. **R** indicates the rotation of the propeller, which stands for “reversed”. It should be mounted on a motor that spins clockwise. **C** is the opposite, should be used with motors that spins counter-clockwise.


* Electronic speed controller (ESC) controls and regulates the speed of an electric brushless motor. All ESCs comes with a rating. The Turnigy Multistar ESC shown below has a rating of 10A, meaning it can draw a maximum continuous current of 10A. Anything higher than 10A will eventually burn or damage the ESC. 

.. image:: ../_static/esc.jpg
   :scale: 30 %
   :align: center

.. note:: 

  Drawing 10A for a long time (~10mins) will heat up the ESC and damage it as well. Always use a higher rating ESC for your setup. E.g. If your motor draws 10A (at full throttle), use either a 12A or a 15A. If the 12A and the 15A ESC weight approximately the same, choose the 15A. A higher rating ESC will prevent overheating. To handle more power, a high rating ESC will be required. As the rating goes up, the weight, size and cost of the ESC go up as well. Always consider how much power you will need by looking up your motor specification (Max current motor drawn). 


* Remote control system. A remote control (RC) radio system is required if you want to manually control your vehicle. In addition to the transmitter/receiver pairs being compatible, the receiver must also be compatible with PX4 and the flight controller hardware.

It's recommended to use Taranis X9D Plus transmitter with X8R receiver as shown below

.. image:: ../_static/frsky_taranis.jpg
   :scale: 90 %
   :align: center


.. image:: ../_static/x8r.jpg
   :scale: 30 %
   :align: center

* UBEC (Universal Battery eliminator circuit) to convert voltage to power Odroid. A BEC is basically a step down voltage regulator. It will take your main battery voltage (e.g. 11.1 Volts) and reduce it down to ~5 Volts to safely power your Odroid and other electronics.

.. image:: ../_static/ubec.jpg
   :scale: 40 %
   :align: center


* Power module. It is the best way to provide power for flight controller unit. It has voltage and current sensors that allows autopilot to estimate remaining battery charge precisely. Usually it comes with every autopilot controller as a default kit. Check official documentations to match right power module to a selected flight controller.

.. image:: ../_static/power_module.jpg
   :scale: 60 %
   :align: center

* LiPo battery. Assuming you know what is the balancer, cell count and voltage, capacity and C-rating.

Assembly process
^^^^^

* Assemble the frame. Attach the power distribution board to it (no need if you use frame with soldered pads).

* Mount the motors to the frame. Mind CW and CCW directions. They should be mounted as follows. We usually use **X** configuration.

.. image:: ../_static/quad_1.jpg
   :scale: 90 %
   :align: center

.. important::

	Do not install propellers now.


* Connect ESCs to motors and plug ESCs to power distribution board (or solder them to the frame). As for now, connect motors to ESCs arbitrary, later you will set them properly by switching any two wires.


* Install power module on the frame. One end should be plugged to power distribution board (or soldered to the frame) and the other end to the battery. DON’T plug it to the battery for now.

* Install flight controller on the frame. Take a look at your flight controller and make sure the arrow is pointing to the front between motor 1 and 3. To mount the controller to the frame, use thick double side tape to damp the vibrations.

* Plug cable from power module to ``POWER`` port of your flight controller.

* Plug buzzer and switch to their corresponding ports on flight controller.

* Connect each of your ESCs servo cables to the corresponding **MAIN OUT** output, eg. motor 1 to **MAIN OUT** port 1.

* Binding process for FrSky X8R

    * Connect the RCIN port from Pixhawk to SBUS port on X8R
    * Turn on the X8R while holding the **F/S** button on the module. Release the button.
    * Press the **Menu** button on your Taranis X9D
    * Go to page 2 by pressing **Page** button.
    * Scroll down with **-** button until you see **Internal RF** line.
    * Select **[Bind]** line, and press **ENT** button. The RED LED on the X8R receiver will flash, indicating the binding process is completed


  .. + Spektrum receiver with autobind 

  ..   1. With the transmitter off, power on the receiver.
  ..   2. The receiver will attempt to connect to the last transmitter it was bound to.
  ..   3. If no transmitter is found it will enter Bind mode, as indicated by a flashing orange LED. If it doesn't, press **Spektrum Bind** button in **Radio** tab.
  ..   4. Press and continue holding bind button, turn on your transmitter and allow the remote receiver to autobind.
  ..   5. When the receiver binds the orange LED turns solid.

  ..   .. important::

  ..     Once the receiver is bound to your transmitter, always power your transmitter on first so the receiver will not enter bind mode. If the model enters bind mode unintentionally, shut off power to the model, ensure the transmitter is powered on with the correct model selected, and then power the model on again. The receiver will not lose its previous bind information if it enters bind mode and does not bind.

  .. + Spektrum receiver without autobind

  ..   1. Use `AR8000 8ch DSMX Receiver <https://www.spektrumrc.com/Products/Default.aspx?ProdID=SPMAR8000>`_.
  ..   2. Insert the bind plug in the ``BATT/BIND`` port on the AR8000 receiver and connect RC receiver to AR8000 receiver.
  ..   3. Power the AR8000 receiver by connecting any AUX port to any Pixhawk MAIN OUT port (motor ports). Note that the LED on the receiver should be flashing, indicating that the receiver is in bind mode and ready to be bound to the transmitter.
  ..   4. Move the sticks and switches on the transmitter to the desired failsafe positions (low throttle and neutral control positions).
  ..   5. Press and continue holding bind button, turn on your transmitter, the system will connect within a few seconds. Once connected, the LED on the receiver will go solid indicating the system is connected.
  ..   6. Remove the bind plug from the ``BATT/BIND`` port on the receiver before you power off the transmitter.
  ..   7. Remove the RC receiver from AR8000, and connect it to Pixhawk via port ``SPKT/DSM``.

* For this stage there’s no need to install Odroid.

Calibration process
-----

* Download ``QGroundControl`` on your computer and open it.

* `Install Stable PX4 firmware <https://docs.px4.io/en/config/firmware.html>`_.

* Set the airframe, for example: Generic 250 Frame, Flamewheel F330 or Flamewheel F450 depending on your frame. Follow steps from this `page <https://docs.px4.io/en/config/airframe.html>`_.

* Calibrate `Compass <https://docs.px4.io/en/config/compass.html>`_, `Accelerometer <https://docs.px4.io/en/config/accelerometer.html>`_, and `Level Horizon <https://docs.px4.io/en/config/level_horizon_calibration.html>`_. 
* Calibrate the `Radio <https://docs.px4.io/en/config/radio.html#performing-the-calibration>`_.

* In ``Flight Modes`` tab under the **Flight Mode Settings** and **Switch settings** sections set:

  - **Mode Channel** to SB (SB switch labeled on your Taranis X9D)
  - **Mode 1: Manual**. 
  - **Mode 4: Altitude**. Climb and drop are controlled to have a maximum rate.
  - **Mode 6: Position**. When sticks are released the vehicle will stop and hold position.
  - **Emergency Kill switch channel** to SF (SF switch labeled on your Taranis X9D). Immediately stops all motor outputs. The vehicle will crash, which may in some circumstances be more desirable than allowing it to continue flying.
  - **Offboard switch channel** to SA (SA switch labeled on your Taranis X9D).

You should have similar as shown in the picture below. Channels for **Flight Mode Settings** and **Switch Settings** might differ.

.. image:: ../_static/qground.png
   :scale: 60 %
   :align: center


.. hint::
  
  If you set everything right, you will see changes in **Flight Mode Settings** section highlighted as yellow. Also, moving sticks, dials and switches will be reported in **Channel Monitor** section.



* In ``Power tab`` write the parameters of your battery (Number of cells), calibrate the battery voltage and ESCs (if you use DJI ESCs, no need to calibrate them).

  * Press **Calculate** on the **Voltage divider** line
  * Measure the voltage with Digital Battery Capacity Checker by connecting it to the battery
  * Enter the the voltage value from the Digital Battery Capacity Checker and press **Calculate** button
  * To calibrate ESC press **Calibrate** under **ESC PWM Minimum and Maximum Calibration** and follow on-screen instructions


* Arm your quadcopter, and check if all motors are rotating in the direction intended. If no, switch any two wires that are connected to ESC. To arm the drone, put the throttle stick in the bottom right corner. This will start the motors on a quadcopter. To disarm, put the throttle stick in the bottom left corner.

* Now you can install propellers. Note that there are CW and CCW propellers as well.

.. danger:: After you install propellers, make sure to keep battery or receiver disconnected while you are working on your quadcopter. Someone may use transmitter bounded to your drone for their own quadcopter as well. The same transmitter can arm several quadcopters!


* Follow this `guide <https://docs.px4.io/en/advanced_config/pid_tuning_guide_multicopter.html>`_ to perform **PID** tuning for your quadcopter if necessary (no need for F330 and F450 frames).


Flying in manual mode
------

* Read `First Flight Guidelines <https://docs.px4.io/en/flying/first_flight_guidelines.html>`_ and `Flying 101 <https://docs.px4.io/en/flying/basic_flying.html>`_.

* Make sure you switch **Kill switch** to off. Select **Manual** as your flight mode.
* Check the battery level, make sure it's enough to perform your first flight.
* Put the quadcopter in the cage and arm. Slowly add throttle while keeping it in the middle of the cage by controlling pitch and yaw.

.. important::
  
  Always check the battery before flying



Odroid installation
------

- Mount Odroid XU4 on the drone

- Solder the UBEC input cable to the power distribution board (or the frame) 

- Solder `Odroid DC Plug Cable <https://www.hardkernel.com/shop/dc-plug-cable-assembly-5-5mm/>`_ to `female servo cable <https://www.sparkfun.com/products/8738>`_ and connect to the UBEC output cable

- In case of MindPX simply connect micro-USB cable to ``USB/OBC`` from the Odroid USB port. In case of Pixhawk use `FTDI module <https://www.ftdichip.com/Support/Documents/DataSheets/Cables/DS_TTL-232R_PCB.pdf>`_. Use `servo cable <https://www.sparkfun.com/products/8738>`_ to solder three wires to GND, TX, and RX (refer to page 8 of the FTDI datasheet file). After that solder these three wires to corresponding **TELEM2** port cable. Note that GND connects to GND, RX to TX, and TX to RX.

- Plug in the DC power cable to the Odroid and check if it's powered from the battery



Troubleshooting
------

* Motors are not rotating while armed and rotates with higher throttle

  - Check ``PWM_MAX`` and ``PWM_MIN`` in parameters and make sure it’s associated with ESCs

* Motor are not rotating or rotating partially.

  - Set ``PWM_RATE`` value to default.

* Drone goes high during take-off and hits the ceiling, even though after take-off the throttle stick is all they way down

  - Try to lower ``MPC_THR_HOVER`` value

Contributors
-----

`Yimeng Lu <https://github.com/luym11>`_ and `Kuat Telegenov <https://github.com/telegek>`_.