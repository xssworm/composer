
add_custom_command(
  OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/core_utils_wrap.cxx
  DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/core_utils.i ${CMAKE_CURRENT_SOURCE_DIR}/resource_provider.h
  COMMAND ${SWIG_COMMAND} -c++ -javascript -jsc
          -I${jsobjects_SWIG_INCLUDE_DIRS}
          -o ${CMAKE_CURRENT_BINARY_DIR}/core_utils_wrap.cxx
          ${CMAKE_CURRENT_SOURCE_DIR}/core_utils.i
)

include_directories(
  ${JS_INCLUDE_DIRS}
  ${BOOST_INCLUDE_DIRS}
  ${jsobjects_INCLUDE_DIRS}
#  ${HIREDIS_INCLUDE_DIRS}
  ${CMAKE_CURRENT_SOURCE_DIR}
)


add_library(core_extensions STATIC
  core_utils_wrap.cxx
  core_utils_initializer.h
  core_utils_initializer.cxx
  resource_provider.h
)

set(core_utils_DIR ${CMAKE_CURRENT_SOURCE_DIR} CACHE INTERNAL "" FORCE)
