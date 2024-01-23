set(example_name decoration)

set(KIT_SRCS main.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

qt5_wrap_cpp(KIT_MOC_CPP ${KIT_MOC_SRCS})

add_executable(${example_name} ${KIT_SRCS} ${KIT_MOC_SRCS})
if(QtPropertyBrowser_BUILD_STATIC)
  target_link_libraries(${example_name} ${PROJECT_NAME}_static)
endif()

if(QtPropertyBrowser_BUILD_SHARED)
  target_link_libraries(${example_name} ${PROJECT_NAME}_share)
endif()

set(KIT_CPP_MOC_SRCS main.cpp)

set(KIT_MOC_CPP)
foreach(file ${KIT_CPP_MOC_SRCS})
  get_filename_component(filename_we ${file} NAME_WE)
  set(output_file ${filename_we}.moc)
  qt5_generate_moc(${file} ${output_file})
  list(APPEND KIT_MOC_CPP ${output_file})
endforeach()

add_custom_target(${example_name}GenerateMoc DEPENDS ${KIT_MOC_CPP})
add_dependencies(${example_name} ${example_name}GenerateMoc)
