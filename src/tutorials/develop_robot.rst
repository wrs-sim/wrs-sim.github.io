
Developing ROBOT PACKAGE
========================

Template of ROBOT PACKAGE
-------------------------

 * `Template robot package <https://github.com/wrs-sim/wrs-robot-template>`_
 * `Template drone package <https://github.com/wrs-sim/wrs-drone-template>`_

STEP1 Create a new directory
-----------------------------

.. code-block:: yaml

 -+- <your_robot> ... any name is ok
    +- controller
      +- CMakeLists.txt ... see ROBOT PACKAGE templates
      +- <your_controller>.cpp ... STEP3
    +- model
      +- <your_robot>.body ... STEP2
    +- project
        +- <your_robot>.cnoid ... STEP4
    +- CMakeLists.txt ... see ROBOT PACKAGE templates
 
STEP2 Create a Body file
------------------------

 * `Choreonoid master documentation: Body File Tutorial <https://choreonoid.org/en/documents/latest/handling-models/modelfile/modelfile-newformat.html>`_

STEP3 Create a SimpleController for Subscriber
----------------------------------------------

 * `Choreonoid master documentation: ROS 2 Mobile Robot Tutorial¶ <https://choreonoid.org/en/documents/latest/ros2/ros2-mobile-robot-tutorial.html>`_

STEP4 Create a Project file
---------------------------

 1. Launch Choreonoid
 2. Open the Body file of STEP2
 3. Add SimpleController of STEP3 as a child item of the loaded Body
 4. Add BodyROS2Item as a child item of the loaded Body
 5. Save a project file

**DO NOT change Body's translation (X, Y) and rotation (R, P, Y) values**


**Create a project file for each robot.**

Edit a YAML file
----------------

Here, we use **wrs-plugin/registration/registration_wrs2025.yaml** as an example of YAML file.
Open the YAML file in any text editor and you should replace the second line as follows:

.. code-block:: yaml
    
    robot_list: &RobotList  [ <Project file name where the custom robot model is saved> ]

When you want to introduce additional custom robot model, you should written RobotList as follows:

.. code-block:: yaml

    robot_list: &RobotList  [ <Project file name where the custom robot model is saved>,  <Project file name where the additional custom robot model is saved> ]

**To swap the positions of your custom robots, change their order in the list.**

Install ROBOT PACKAGE
---------------------

**Move ROBOT PACKAGE to choreonoid/ext/.**
Additionally, when you want to use your own UGV, edit share/default/materials.yaml. Replace "YourRobot" on line 212 with the body name of your own UGV, and replace "CHASSIS" on line 213 with the root link of your own UGV.

.. code-block:: yaml

    reference_body: YourRobot
    reference_link: CHASSIS

Then, rebuild Choreonoid for cloning your model and project files, and for compling your controller files.

.. code-block:: bash
   
   $ cd ~/ros2_ws
   $ colcon build --symlink-install --cmake-args -DBUILD_AGX_DYNAMICS_PLUGIN=ON -DBUILD_AGX_BODYEXTENSION_PLUGIN=ON -DBUILD_SCENE_EFFECTS_PLUGIN=ON -DBUILD_HAIRO_WORLD_PLUGIN=ON -DENABLE_INSTALL_RPATH_USE_LINK_PATH=ON –cmake-clean-cache

**When you want to update your model, project and controller files, you should build Choreonoid again.**

Run Choreonoid
--------------

.. code-block:: bash
    
    $ cd ~
    $ cd ~/ros2_ws
    $ source install/setup.bash
    $ ros2 run choreonoid_ros choreonoid ~/ros2_ws/src/choreonoid/ext/wrs-plugin/registration/registration_wrs2025.yaml --wrs-util testrun
