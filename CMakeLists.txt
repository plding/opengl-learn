cmake_minimum_required (VERSION 2.8)
project (LearnOpenGL)

list(APPEND CMAKE_CXX_FLAGS "-std=c++11")

# find the required packages
find_package(OpenGL REQUIRED)
find_package(GLFW3 REQUIRED)
find_package(GLM REQUIRED)

include_directories(/usr/local/include)
include_directories(/usr/local/Cellar/glew/2.1.0/include)

link_directories(/usr/local/Cellar/glew/2.1.0/lib)
link_directories(/usr/local/Cellar/glfw/3.3/lib)
link_directories(/usr/local/Cellar/glm/0.9.9.5/lib)

find_library(OpenGL_LIBRARY OpenGL)
set(LIBS ${OPENGL_LIBRARY} glew glfw)

set(CHAPTERS
    1.getting_started
)

set(1.getting_started
    1.1.hello_window
    1.2.hello_window_clear
    2.1.hello_triangle
)

# then create a project file per tutorial
foreach(CHAPTER ${CHAPTERS})
    foreach(DEMO ${${CHAPTER}})
        file(GLOB SOURCE
            "src/${CHAPTER}/${DEMO}/*.h"
            "src/${CHAPTER}/${DEMO}/*.cpp"
        )
        set(NAME "${CHAPTER}__${DEMO}")
        add_executable(${NAME} ${SOURCE})
        target_link_libraries(${NAME} ${LIBS})
    endforeach(DEMO)
endforeach(CHAPTER)
