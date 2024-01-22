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
  
SET(libname ${PROJECT_NAME})

if(QtPropertyBrowser_BUILD_SHARE) 
  add_definitions(-DQT_QTPROPERTYBROWSER_EXPORT)

  ADD_LIBRARY(${libname}_share SHARED 
  ${KIT_SRCS} 
  ${KIT_UI_FORMS} 
  ${KIT_resources}
  )
  TARGET_LINK_LIBRARIES(${libname}_share 
  ${QT_LIBRARIES}
  )
endif(QtPropertyBrowser_BUILD_SHARE)

if(QtPropertyBrowser_BUILD_STATIC)
  ADD_LIBRARY(${libname}_static STATIC 
  ${KIT_SRCS} 
  ${KIT_UI_FORMS} 
  ${KIT_resources}
  )
  TARGET_LINK_LIBRARIES(${libname}_static 
  ${QT_LIBRARIES}
  )
endif(QtPropertyBrowser_BUILD_STATIC)
