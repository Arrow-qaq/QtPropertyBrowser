add_definitions(-DQT_DISABLE_DEPRECATED_BEFORE=0)
SET(KIT_SRCS
  qtbuttonpropertybrowser.cpp
  qtbuttonpropertybrowser.h
  qteditorfactory.cpp
  qteditorfactory.h
  qtgroupboxpropertybrowser.cpp
  qtgroupboxpropertybrowser.h
  qtpropertybrowser.cpp
  qtpropertybrowser.h
  qtpropertybrowserutils.cpp
  qtpropertybrowserutils_p.h
  qtpropertymanager.cpp
  qtpropertymanager.h
  qttreepropertybrowser.cpp
  qttreepropertybrowser.h
  qtvariantproperty.cpp
  qtvariantproperty.h
  )

SET(KIT_MOC_SRCS
  qtpropertybrowserutils_p.h
  )

SET(KIT_UI_FORMS
  )

SET(KIT_resources
  qtpropertybrowser.qrc
  )
  
INCLUDE_DIRECTORIES(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}
  )
  
QT5_WRAP_UI(KIT_UI_CPP ${KIT_UI_FORMS})
QT5_WRAP_CPP(KIT_MOC_CPP ${KIT_MOC_SRCS})
QT5_ADD_RESOURCES(KIT_QRC_SRCS ${KIT_resources})

SET(libname ${PROJECT_NAME})

if(QtPropertyBrowser_BUILD_SHARE) 
  add_definitions(-DQT_QTPROPERTYBROWSER_EXPORT)

  ADD_LIBRARY(${libname}_share SHARED 
  ${KIT_SRCS} 
  ${KIT_UI_CPP} 
  ${KIT_MOC_CPP} 
  ${KIT_QRC_SRCS}
  )
  TARGET_LINK_LIBRARIES(${libname}_share 
  ${QT_LIBRARIES}
  )
endif(QtPropertyBrowser_BUILD_SHARE)

if(QtPropertyBrowser_BUILD_STATIC)
  ADD_LIBRARY(${libname}_static STATIC 
  ${KIT_SRCS} 
  ${KIT_UI_CPP} 
  ${KIT_MOC_CPP} 
  ${KIT_QRC_SRCS}
  )
  TARGET_LINK_LIBRARIES(${libname}_static 
  ${QT_LIBRARIES}
  )
endif(QtPropertyBrowser_BUILD_STATIC)
  

# List of header that should go though moc
SET(KIT_HEADERS_MOC_SRCS
  qtbuttonpropertybrowser.h
  qteditorfactory.h
  qtgroupboxpropertybrowser.h
  qtpropertybrowser.h
  qtpropertybrowserutils_p.h
  qtpropertymanager.h
  qttreepropertybrowser.h
  qtvariantproperty.h
  )

SET(KIT_MOC_CPP)
FOREACH(file ${KIT_HEADERS_MOC_SRCS})
  get_filename_component(filename_we ${file} NAME_WE)
  SET(output_file moc_${filename_we}.cpp)
  QT5_GENERATE_MOC(${file} ${output_file})
  LIST(APPEND KIT_MOC_CPP ${output_file})
ENDFOREACH()

# List of cpp files that should go though moc
SET(KIT_CPP_MOC_SRCS
  qteditorfactory.cpp
  qtpropertymanager.cpp
  qttreepropertybrowser.cpp
  )

FOREACH(file ${KIT_CPP_MOC_SRCS})
  get_filename_component(filename_we ${file} NAME_WE)
  SET(output_file ${filename_we}.moc)
  QT5_GENERATE_MOC(${file} ${output_file})
  LIST(APPEND KIT_MOC_CPP ${output_file})
ENDFOREACH()

add_custom_target(${libname}GenerateMoc
  DEPENDS ${KIT_MOC_CPP}
  )

if(QtPropertyBrowser_BUILD_SHARE) 
  add_dependencies(${libname}_share ${libname}GenerateMoc)
endif(QtPropertyBrowser_BUILD_SHARE)
if(QtPropertyBrowser_BUILD_STATIC)
  add_dependencies(${libname}_static ${libname}GenerateMoc)  
endif(QtPropertyBrowser_BUILD_STATIC)
