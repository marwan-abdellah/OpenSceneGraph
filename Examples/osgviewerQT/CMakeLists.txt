SET(TARGET_SRC 
    QOSGWidget.cpp
    AdapterWidget.cpp
    osgviewerQT.cpp
)

IF   (QT4_FOUND)
    SET(TARGET_EXTERNAL_LIBRARIES ${QT_QTCORE_LIBRARY_RELEASE} ${QT_QTGUI_LIBRARY_RELEASE} ${QT_QTOPENGL_LIBRARY_RELEASE} )
    ADD_DEFINITIONS(-DUSE_QT4)
ELSE(QT4_FOUND)
    SET(TARGET_EXTERNAL_LIBRARIES ${QT_LIBRARIES} )
ENDIF(QT4_FOUND)

INCLUDE_DIRECTORIES(${QT_INCLUDE_DIR} )

#### end var setup  ###
SETUP_EXAMPLE(osgviewerQT)
