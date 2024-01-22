
SET(example_name simple)

SET(KIT_SRCS
  main.cpp
  )
  
INCLUDE_DIRECTORIES(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}
  )
  
ADD_EXECUTABLE(${example_name} ${KIT_SRCS})

if(QtPropertyBrowser_BUILD_STATIC)
  TARGET_LINK_LIBRARIES(${example_name} ${PROJECT_NAME}_static)
endif()

if(QtPropertyBrowser_BUILD_SHARED)
  TARGET_LINK_LIBRARIES(${example_name} ${PROJECT_NAME}_share)
endif()

