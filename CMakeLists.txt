cmake_minimum_required(VERSION 3.0.2)
project(vanguard_bms)

find_package(catkin REQUIRED COMPONENTS
  diagnostic_msgs
  sensor_msgs
)

catkin_package()

catkin_install_python(PROGRAMS
  scripts/driver
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

install(DIRECTORY launch config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

if (CATKIN_ENABLE_TESTING)
  find_package(roslint)
  set(ROSLINT_PYTHON_OPTS --ignore=E121,E123,E126,E226,E24,E251,E704,W503,W504)
  roslint_python(scripts/driver)
  roslint_add_test()

  find_package(roslaunch)
  roslaunch_add_file_check(launch/bms.launch)
endif()
