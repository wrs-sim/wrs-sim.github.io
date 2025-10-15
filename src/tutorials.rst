
Tutorials
=========

Requirements
------------

 * Ubuntu 22.04 LTS (Humble Hawksbill)

Installing ROS2
---------------

Setup Sources
^^^^^^^^^^^^^

.. code-block:: bash
   
   $ sudo apt install software-properties-common
   $ sudo add-apt-repository universe
   $ sudo apt update && sudo apt install curl -y
   $ export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
   $ curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
   $ sudo dpkg -i /tmp/ros2-apt-source.deb

Install ROS 2 packages
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

   $ sudo apt update
   $ sudo apt upgrade
   $ sudo apt install ros-humble-desktop
   $ sudo apt install ros-dev-tools
   $ sudo apt install python3-colcon-clean
   $ sudo apt install ros-humble-compressed-image-transport
   $ sudo apt install python3-colcon-common-extensions

Environment setup
^^^^^^^^^^^^^^^^^

.. code-block:: bash

   $ source /opt/ros/humble/setup.bash

or

.. code-block:: bash

   $ echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
   $ source ~/.bashrc

Initialize rosdep
^^^^^^^^^^^^^^^^^

.. code-block:: bash
   
   $ sudo rosdep init
   $ rosdep update

Developing ROBOT PACKAGE
------------------------

Template of ROBOT PACKAGE
^^^^^^^^^^^^^^^^^^^^^^^^^

 * `Template robot package <https://github.com/wrs-sim/wrs-robot-template>`_
 * `Template drone package <https://github.com/wrs-sim/wrs-drone-template>`_

References for making Body file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 * `Choreonoid master documentation: ROS 2 Mobile Robot Tutorial¶ <https://choreonoid.org/en/documents/latest/ros2/ros2-mobile-robot-tutorial.html>`_
 * `Choreonoid master documentation: Body File Tutorial <https://choreonoid.org/en/documents/latest/handling-models/modelfile/modelfile-newformat.html>`_

Building Choreonoid competition version
---------------------------------------

Create a new directory
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
   
   $ mkdir -p ~/ros2_ws/src
   $ cd ~/ros2_ws/src

Clone source repo
^^^^^^^^^^^^^^^^^

.. code-block:: bash
   
   $ cd ~/ros2_ws/src
   $ git clone https://github.com/choreonoid/choreonoid.git
   $ git clone https://github.com/choreonoid/choreonoid_ros.git
   $ git clone --recursive https://github.com/wrs-sim/wrs-plugin choreonoid/ext/wrs-plugin
   $ git clone https://github.com/wrs-sim/choreonoid_joy2.git

Resolve dependencies
^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
   
   $ rosdep install -y --from-paths ~/ros2_ws/src --ignore-src

AGX Dynamics installation reference
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 * `Choreonoid master documentation: Installation of AGX Dynamics (Ubuntu Linux) <https://choreonoid.org/en/documents/latest/agxdynamics/install/install-agx-ubuntu.html>`_
 * `Tutorial video <https://www.youtube.com/watch?v=SxmwYl_gPEY>`_

HAIROWorldPlugin installation reference
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please obtain this software before building Choreonoid's WRS environment specification. Competitors are requested to contact the competition secretariat. Others should contact JAEA Suzuki at "suzuki.kenta38[a]jaea.go.jp". (Change the [a] to @ when you send us an email.)
**Move hairo-world-plugin to choreonoid/ext/.**

Install ROBOT PACKAGE
^^^^^^^^^^^^^^^^^^^^^

**Move ROBOT PACKAGE to choreonoid/ext/.**
Additionally, when you want to use your own UGV, edit share/default/materials.yaml. Replace "YourRobot" on line 212 with the body name of your own UGV, and replace "CHASSIS" on line 213 with the root link of your own UGV.

.. code-block:: yaml

    reference_body: YourRobot
    reference_link: CHASSIS

Install requisites
^^^^^^^^^^^^^^^^^^

.. code-block:: bash
   
   $ choreonoid/misc/script/install-requisites-ubuntu-22.04.sh
   $ sudo ./choreonoid/ext/hairo-world-plugin/misc/script/install-requisites-ubuntu-22.04.sh

Build Choreonoid
^^^^^^^^^^^^^^^^

.. code-block:: bash
   
   $ cd ~/ros2_ws
   $ colcon build --symlink-install --cmake-args -DBUILD_AGX_DYNAMICS_PLUGIN=ON -DBUILD_AGX_BODYEXTENSION_PLUGIN=ON -DBUILD_SCENE_EFFECTS_PLUGIN=ON -DBUILD_HAIRO_WORLD_PLUGIN=ON -DENABLE_INSTALL_RPATH_USE_LINK_PATH=ON

**By building Choreonoid, your model and project files will be cloned to install directory, and your controller files will be compiled. When you want to update your model, project and controller files, you should build Choreonoid again.**

References for building Choreonoid
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 * `Choreonoid master documentation: ROS 2 Integration <https://choreonoid.org/en/documents/latest/ros2/index.html>`_

Running Choreonoid
------------------

.. code-block:: bash
   
   $ cd ~
   $ cd ~/ros2_ws
   $ source install/setup.bash
   $ ros2 run choreonoid_ros choreonoid ~/ros2_ws/src/choreonoid/ext/wrs-plugin/registration/registration_wrs2020.yaml --wrs-util ts1

.. list-table:: Detail of YAML files
   :widths: 15 10 30
   :header-rows: 1

   * - YAML file
     - Arguments
     - Description
   * - registration_wrs2020.yaml
     - ts1
     - Load WRS2020 TS1 environment
   * - registration_wrs2020.yaml
     - ts2
     - Load WRS2020 TS2 environment
   * - registration_wrs2020.yaml
     - ts3
     - Load WRS2020 TS3 environment
   * - registration_wrs2020.yaml
     - ts4
     - Load WRS2020 TS4 environment
   * - registration_wrs2025.yaml
     - testrun
     - Load WRS2025 test run environment
   * - registration_wrs2025.yaml
     - ps1
     - Load WRS2025 PS-1 environment
   * - registration_wrs2025.yaml
     - ps2
     - Load WRS2025 PS-2 environment
   * - registration_wrs2025.yaml
     - ps3
     - Load WRS2025 PS-3 environment
   * - registration_wrs2025.yaml
     - ps4
     - Load WRS2025 PS-4 environment
   * - registration_wrs2025.yaml
     - ps12
     - Load WRS2025 PS-12 environment
   * - registration_wrs2025.yaml
     - ps34
     - Load WRS2025 PS-34 environment
