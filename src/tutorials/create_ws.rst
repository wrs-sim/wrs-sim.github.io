
Creating a workspace
====================

Create a new directory
----------------------

.. code-block:: bash
   
   $ mkdir -p ~/ros2_ws/src
   $ cd ~/ros2_ws/src

Clone source repo
-----------------

.. code-block:: bash
   
   $ cd ~/ros2_ws/src
   $ git clone https://github.com/choreonoid/choreonoid.git
   $ git clone https://github.com/choreonoid/choreonoid_ros.git
   $ git clone --recursive https://github.com/wrs-sim/wrs-plugin choreonoid/ext/wrs-plugin
   $ git clone https://github.com/wrs-sim/choreonoid_joy2.git

Resolve dependencies
--------------------

.. code-block:: bash
   
   $ rosdep install -y --from-paths ~/ros2_ws/src --ignore-src

AGX Dynamics installation reference
-----------------------------------

 * `Choreonoid master documentation: Installation of AGX Dynamics (Ubuntu Linux) <https://choreonoid.org/en/documents/latest/agxdynamics/install/install-agx-ubuntu.html>`_
 * `Tutorial video: Installing AGX Dynamics <https://www.youtube.com/watch?v=SxmwYl_gPEY>`_

HAIROWorldPlugin installation reference
---------------------------------------

Please obtain this software before building Choreonoid's WRS environment specification. Competitors are requested to contact the competition secretariat. Others should contact JAEA Suzuki at "suzuki.kenta38[a]jaea.go.jp". (Change the [a] to @ when you send us an email.)
**Move hairo-world-plugin to choreonoid/ext/.**

Install requisites
------------------

.. code-block:: bash
   
   $ choreonoid/misc/script/install-requisites-ubuntu-22.04.sh

Build Choreonoid
----------------

.. code-block:: bash
   
   $ cd ~/ros2_ws
   $ colcon build --symlink-install --cmake-args -DBUILD_AGX_DYNAMICS_PLUGIN=ON -DBUILD_AGX_BODYEXTENSION_PLUGIN=ON -DBUILD_SCENE_EFFECTS_PLUGIN=ON -DBUILD_HAIRO_WORLD_PLUGIN=ON -DENABLE_INSTALL_RPATH_USE_LINK_PATH=ON

References
----------

 * `Choreonoid master documentation: ROS 2 Integration <https://choreonoid.org/en/documents/latest/ros2/index.html>`_
