
Installing ROS2(Humble Hawksbill)
=================================

Platform
--------

 * Ubuntu 22.04 LTS

Setup Sources
-------------

.. code-block:: bash
   
   $ sudo apt install software-properties-common
   $ sudo add-apt-repository universe
   $ sudo apt update && sudo apt install curl -y
   $ export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
   $ curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
   $ sudo dpkg -i /tmp/ros2-apt-source.deb

Install ROS 2 packages
----------------------

.. code-block:: bash

   $ sudo apt update
   $ sudo apt upgrade
   $ sudo apt install ros-humble-desktop
   $ sudo apt install ros-dev-tools
   $ sudo apt install python3-colcon-clean
   $ sudo apt install ros-humble-compressed-image-transport
   $ sudo apt install python3-colcon-common-extensions

Environment setup
-----------------

.. code-block:: bash

   $ echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
   $ source ~/.bashrc

Initialize rosdep
-----------------

.. code-block:: bash
   
   $ sudo rosdep init
   $ rosdep update

References
----------

 * `ROS 2 Documentation: Ubuntu (deb packages) <https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html>`_
