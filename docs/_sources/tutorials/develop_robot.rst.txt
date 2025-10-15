
Developing ROBOT PACKAGE
========================

Template of ROBOT PACKAGE
-------------------------

 * `Template robot package <https://github.com/wrs-sim/wrs-robot-template>`_
 * `Template drone package <https://github.com/wrs-sim/wrs-drone-template>`_

Create a new directory
----------------------

Now editing...

Create a Body file
------------------

 * `Choreonoid master documentation: Body File Tutorial <https://choreonoid.org/en/documents/latest/handling-models/modelfile/modelfile-newformat.html>`_

Create a Project file
---------------------

Now editing...

Create a SimpleController
-------------------------

 * `Choreonoid master documentation: ROS 2 Mobile Robot Tutorial¶ <https://choreonoid.org/en/documents/latest/ros2/ros2-mobile-robot-tutorial.html>`_

Edit a YAML file
----------------

Now editing...

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
   $ colcon build --symlink-install --cmake-args -DBUILD_AGX_DYNAMICS_PLUGIN=ON -DBUILD_AGX_BODYEXTENSION_PLUGIN=ON -DBUILD_SCENE_EFFECTS_PLUGIN=ON -DBUILD_HAIRO_WORLD_PLUGIN=ON -DENABLE_INSTALL_RPATH_USE_LINK_PATH=ON

**When you want to update your model, project and controller files, you should build Choreonoid again.**

Run Choreonoid
--------------

Now editing...
