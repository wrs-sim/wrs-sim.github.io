
Running Choreonoid
==================

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
