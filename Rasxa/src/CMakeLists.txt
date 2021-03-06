add_executable(RasxaApp 

    main.cpp 

    PortAudioMicrophoneWrapper.cpp 

    InteractionManager.cpp 

    UserInputManager.cpp

    ConsolePrinter.cpp

    GuiRenderer.cpp

    UIManager.cpp

    KeywordObserver.cpp

    ConnectionObserver.cpp

    RasxaApplication.cpp)



target_include_directories(RasxaApp PUBLIC 

    "${SampleApp_SOURCE_DIR}/include"

    "${MediaPlayer_SOURCE_DIR}/include"

    "${DefaultClient_SOURCE_DIR}/include"

    "${AudioResources_SOURCE_DIR}/include"

    "${PORTAUDIO_INCLUDE_DIR}")



target_link_libraries(RasxaApp 

    DefaultClient

    AuthDelegate 

    MediaPlayer 

    "${PORTAUDIO_LIB_PATH}")



if(KITTAI_KEY_WORD_DETECTOR)

    target_link_libraries(RasxaApp 

        KITTAI)

endif()



if(SENSORY_KEY_WORD_DETECTOR)

    target_link_libraries(RasxaApp SENSORY)

endif()



if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

    target_link_libraries(RasxaApp

        "-framework CoreAudio" 

        "-framework AudioToolbox" 

        "-framework AudioUnit" 

        "-framework CoreServices" 

        "-framework Carbon")

elseif(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

    target_link_libraries(RasxaApp

        rt m pthread asound)

elseif(${CMAKE_SYSTEM_NAME} MATCHES "Windows")

    message(FATAL_ERROR "Windows is unsupported at the moment")  

endif()
