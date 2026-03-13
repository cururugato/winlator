# CMakeLists.txt simplificado para Winlator (sem OpenXR-SDK nem SDL2)

cmake_minimum_required(VERSION 3.18)

project(winlator LANGUAGES C CXX)

# Definições básicas
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Desativa subdiretórios externos temporariamente
# add_subdirectory(OpenXR-SDK)
# add_subdirectory(sdl2)

# Adiciona os sources do app
file(GLOB_RECURSE WINLATOR_SRC
    "${CMAKE_SOURCE_DIR}/src/main/cpp/*.cpp"
    "${CMAKE_SOURCE_DIR}/src/main/cpp/*.c"
)

# Cria a biblioteca compartilhada (.so)
add_library(winlator SHARED ${WINLATOR_SRC})

# Inclui headers do app
target_include_directories(winlator PRIVATE
    "${CMAKE_SOURCE_DIR}/src/main/cpp"
)

# Configura para Android
find_library(log-lib log)

target_link_libraries(winlator PRIVATE ${log-lib})

# Mensagens de debug
message(STATUS "Winlator source files: ${WINLATOR_SRC}")
