# Copyright 2015 Software Radio Systems Limited
#
# This file is part of srsUE
#
# srsUE is free software: you can redistribute it and/or modify
# it under the terms of the GNU Affero General Public License as
# published by the Free Software Foundation, either version 3 of
# the License, or (at your option) any later version.
#
# srsUE is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU Affero General Public License for more details.
#
# A copy of the GNU Affero General Public License can be found in
# the LICENSE file in the top-level directory of this distribution
# and at http://www.gnu.org/licenses/.
#

add_subdirectory(radio)
add_subdirectory(common)
add_subdirectory(phy)
add_subdirectory(mac)
add_subdirectory(upper)

add_executable(ue main.cc ue.cc metrics_stdout.cc)
target_link_libraries(ue    srsue_upper
                            srsue_common
                            srsue_mac
                            srsue_phy
                            srsue_radio
                            lte
                            ${CMAKE_THREAD_LIBS_INIT}
                            ${Boost_LIBRARIES})


########################################################################
# Option to run command after build (useful for remote builds)
########################################################################
if (NOT ${BUILD_CMD} STREQUAL "")
  message(STATUS "Added custom post-build command: ${BUILD_CMD}")
  add_custom_command(TARGET ue POST_BUILD COMMAND ${BUILD_CMD})
else(NOT ${BUILD_CMD} STREQUAL "")
  message(STATUS "No post-build command defined")
endif (NOT ${BUILD_CMD} STREQUAL "")
