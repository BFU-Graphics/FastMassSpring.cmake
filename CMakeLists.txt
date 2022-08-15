cmake_minimum_required(VERSION 3.20)
project(FastMassSpring)

file(GLOB SRCS src/*.cpp src/*.h src/*.c)
add_executable(FastMassSpring ${SRCS})

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)
target_link_libraries(FastMassSpring PRIVATE Threads::Threads) # std::thread need pthread lib to be linked

find_package(GLUT REQUIRED)
target_link_libraries(FastMassSpring PRIVATE GLUT::GLUT)

find_package(GLEW REQUIRED)
target_link_libraries(FastMassSpring PRIVATE GLEW::GLEW)

find_package(glm CONFIG REQUIRED)
target_link_libraries(FastMassSpring PRIVATE glm::glm)

find_package(tinyxml CONFIG REQUIRED)
target_link_libraries(FastMassSpring PRIVATE unofficial-tinyxml::unofficial-tinyxml)

find_package(Eigen3 CONFIG REQUIRED)
target_link_libraries(FastMassSpring PRIVATE Eigen3::Eigen)

include_directories(AntTweakBar/include)
target_link_directories(FastMassSpring PRIVATE AntTweakBar/lib)
target_link_libraries(FastMassSpring PRIVATE AntTweakBar64)

if (NOT EXISTS ${CMAKE_BINARY_DIR}/config)
    file(COPY config DESTINATION ${CMAKE_BINARY_DIR})
endif ()
if (NOT EXISTS ${CMAKE_BINARY_DIR}/scenes)
    file(COPY scenes DESTINATION ${CMAKE_BINARY_DIR})
endif ()
if (NOT EXISTS ${CMAKE_BINARY_DIR}/shaders)
    file(COPY shaders DESTINATION ${CMAKE_BINARY_DIR})
endif ()
if (NOT EXISTS ${CMAKE_BINARY_DIR}/textures)
    file(COPY textures DESTINATION ${CMAKE_BINARY_DIR})
endif ()
if (NOT EXISTS ${CMAKE_BINARY_DIR}/mesh_models)
    file(COPY mesh_models DESTINATION ${CMAKE_BINARY_DIR})
endif ()
if (NOT EXISTS ${CMAKE_BINARY_DIR}/obj_models)
    file(COPY obj_models DESTINATION ${CMAKE_BINARY_DIR})
endif ()
if (NOT EXISTS ${CMAKE_BINARY_DIR}/AntTweakBar64.dll)
    file(COPY AntTweakBar/lib/AntTweakBar64.dll DESTINATION ${CMAKE_BINARY_DIR})
endif ()
