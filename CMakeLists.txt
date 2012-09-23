# @@@LICENSE
#
# Copyright (c) 2007-2012 Hewlett-Packard Development Company, L.P.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# LICENSE@@@

cmake_minimum_required(VERSION 2.8.7)

project(webos-initscripts NONE)

include(webOS/webOS)
webos_modules_init(1 0 0 QUALIFIER RC3)
webos_component(2 0 0)

webos_machine_impl_dep()

# Not installing control-alt-delete or rc0 here are they are
# already installed on the emulators.

set(configurelist 
     files/launch/banner
     files/launch/bootmisc
     files/launch/cgroups
     files/launch/console
     files/launch/crond
     files/launch/devpts
     files/launch/finish
     files/launch/hostname
     files/launch/modutils
     files/launch/mountall
     files/launch/networking
     files/launch/populate-volatile
     files/launch/reboot
     files/launch/start_update
     files/launch/sysfs
     files/launch/timezone
     files/launch/tokens
     files/launch/udev
     files/launch/urandom
     files/launch/usbctrl)

foreach (confitem ${configurelist})
	webos_build_configured_file(${confitem} UPSTARTCONFDIR "")
endforeach()

if(${WEBOS_TARGET_MACHINE_IMPL} STREQUAL simulator)
	webos_build_configured_file(files/launch/swaphack SYSCONFDIR event.dis)
else()
	webos_build_configured_file(files/launch/swaphack SYSCONFDIR event.d)
endif(${WEBOS_TARGET_MACHINE_IMPL} STREQUAL simulator)

webos_build_configured_file(scripts/public/reboot_ls-hubd_if.sh SBINDIR "")

install(DIRECTORY DESTINATION @WEBOS_INSTALL_UPSTARTCONFDIR@/finish-poststart.d)

# Not installing files/launch/rcS as it is already installed on the emulator
install(FILES
        files/launch/alignment
        DESTINATION @WEBOS_INSTALL_UPSTARTCONFDIR@ )

