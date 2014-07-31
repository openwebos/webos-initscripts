# @@@LICENSE
#
# Copyright (c) 2007-2014 LG Electronics, Inc.
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
webos_modules_init(1 0 0 QUALIFIER RC7)
webos_component(3 0 0)

webos_machine_impl_dep()

webos_configure_source_files(configurelist 
    files/launch/banner.conf
    files/launch/bootmisc.conf
    files/launch/cgroups.conf
    files/launch/crond.conf
    files/launch/init-boot-done.conf
    files/launch/modutils.conf
    files/launch/mountall.conf
    files/launch/networking.conf
    files/launch/populate-volatile.conf
    files/launch/reboot.conf
    files/launch/SetInitEnv.conf
    files/launch/start_update.conf
    files/launch/timezone.conf
    files/launch/udev.conf
    files/launch/urandom.conf
    files/launch/usbctrl.conf)

install(FILES ${configurelist} DESTINATION ${WEBOS_INSTALL_SYSCONFDIR}/init)
# unconfigured job files:
install(FILES files/launch/alignment.conf files/launch/console.conf files/launch/devpts.conf files/launch/sysctl.conf DESTINATION ${WEBOS_INSTALL_SYSCONFDIR}/init)

install(DIRECTORY DESTINATION ${WEBOS_INSTALL_SYSCONFDIR}/init/finish-poststart.d)

