set(URBI_ROOT_DIR "/usr" CACHE PATH "Urbi root directory.")

find_package (PkgConfig REQUIRED)
find_package (Urbi REQUIRED)

#set (BOOST_ROOT ${URBI_ROOT_DIR})
find_package (Boost REQUIRED)

pkg_search_module (playerc++ REQUIRED playerc++)

include_directories (${playerc++_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS} ${URBI_INCLUDE_DIRS})
add_library (urobotflash SHARED urobotflash.cpp)
target_link_libraries (urobotflash ${playerc++_LIBRARIES} ${URBI_LIBRARIES} ${Boost_LIBRARIES})

set_target_properties (urobotflash PROPERTIES
  VERSION 0.0.1
  SOVERSION 0.0.1)

install (TARGETS urobotflash DESTINATION lib/gostai/uobjects COMPONENT libraries)

configure_file (test.u.in test.u COPYONLY)
