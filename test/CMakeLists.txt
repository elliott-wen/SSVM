# SPDX-License-Identifier: Apache-2.0

if (NOT SSVM_DISABLE_AOT_RUNTIME)
  add_subdirectory(aot)
endif()
add_subdirectory(spec)
add_subdirectory(ast)
add_subdirectory(loader)
add_subdirectory(interpreter)
add_subdirectory(host/ssvm_process)
add_subdirectory(host/wasi)
add_subdirectory(externref)
add_subdirectory(expected)
add_subdirectory(span)
add_subdirectory(po)

if(BUILD_COVERAGE)
  setup_target_for_coverage_gcovr_html(
    NAME coverage
    EXECUTABLE ctest -j ${PROCESSOR_COUNT}
    DEPENDENCIES ssvm
    BASE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
    EXCLUDE
      "${PROJECT_SOURCE_DIR}/thirdparty/*"
      "${PROJECT_SOURCE_DIR}/test/*"
    )
  setup_target_for_coverage_gcovr_xml(
    NAME codecov
    EXECUTABLE ctest -j ${PROCESSOR_COUNT}
    DEPENDENCIES ssvm
    BASE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
    EXCLUDE
      "${PROJECT_SOURCE_DIR}/thirdparty/*"
      "${PROJECT_SOURCE_DIR}/test/*"
    )

endif()
