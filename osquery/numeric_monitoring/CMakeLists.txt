# Copyright (c) 2018-present, Trail of Bits, Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

cmake_minimum_required(VERSION 3.13.1)

function(osquery_numericmonitoring_main)
  add_subdirectory("plugins")
  generateOsqueryNumericmonitoring()
endfunction()

function(generateOsqueryNumericmonitoring)
  add_library(osquery_numericmonitoring EXCLUDE_FROM_ALL
    numeric_monitoring.cpp
    plugin_interface.cpp
    pre_aggregation_cache.cpp
  )

  target_link_libraries(osquery_numericmonitoring PUBLIC
    global_cxx_settings
    osquery_core
    osquery_utils
    thirdparty_boost
  )

  set(public_header_files
    plugin_interface.h
    pre_aggregation_cache.h
  )

  generateIncludeNamespace(osquery_numericmonitoring "osquery/numeric_monitoring" "FILE_ONLY" ${public_header_files})
endfunction()

osquery_numericmonitoring_main()