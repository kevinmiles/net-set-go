SET(LIB_NAME NetCore)

SET(SOURCE_DIR ${SOURCE_PATH}/NetSetGo/${LIB_NAME})
SET(HEADER_DIR ${HEADER_PATH}/NetSetGo/${LIB_NAME})

ADD_SOURCE_FILES(LIB_SOURCE_FILES ${SOURCE_DIR} "")

ADD_HEADER_FILES(LIB_HEADER_FILES ${HEADER_DIR} "")

SET(LIB_TYPE SHARED)

ADD_LIBRARY(${LIB_NAME}
            ${LIB_TYPE}
            ${LIB_SOURCE_FILES}
            ${LIB_HEADER_FILES}
)

INCLUDE_DIRECTORIES(${HEADER_PATH}
                    # todo: add more
)

#Windows libraries to link into the executable, both Release and Debug
IF (MSVC)
   TARGET_LINK_LIBRARIES(${LIB_NAME}
                         ws2_32)
ENDIF (MSVC)

SET_TARGET_PROPERTIES(${LIB_NAME} PROPERTIES DEFINE_SYMBOL NETCORE)

SET_TARGET_PROPERTIES(${LIB_NAME} 
                      PROPERTIES FRAMEWORK TRUE 
                      PUBLIC_HEADER "${LIB_HEADER_FILES}"
)

IF (NOT APPLE)
INSTALL(TARGETS ${LIB_NAME}
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_PREFIX}/include/${LIB_NAME}
)
ENDIF (NOT APPLE)
