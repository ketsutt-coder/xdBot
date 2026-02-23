cmake_minimum_required(VERSION 3.25) # Geode 5 recomienda 3.25+

# NO definas CMAKE_OSX_ARCHITECTURES manualmente aquí, 
# Geode lo maneja automáticamente según el target.
project(xdBot2 VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Configuración de Geode (Buscando el SDK)
if (NOT DEFINED ENV{GEODE_SDK})
    # Intenta buscarlo si no está la variable de entorno (útil para setups locales)
    find_package(Geode REQUIRED)
else()
    add_subdirectory($ENV{GEODE_SDK} ${CMAKE_CURRENT_BINARY_DIR}/geode)
endif()

# Definición de la librería
# Nota: Usamos una variable para los archivos para que sea más fácil de leer
set(MOD_SOURCES
    src/main.cpp
    src/global.cpp
    src/macro.cpp
    src/keybinds.cpp
    src/utils/utils.cpp
    src/gdr/gdr.cpp
    src/renderer/renderer.cpp
    src/hacks/other.cpp
    src/hacks/tps_bypass.cpp
    src/hacks/frame_stepper.cpp
    src/hacks/layout_mode.cpp
    src/hacks/show_trajectory.cpp
    src/hacks/coin_finder.cpp
    src/hacks/clickbot.cpp
    src/hacks/autoclicker.cpp
    src/ui/macro_editor.cpp
    src/ui/button_edit_layer.cpp
    src/ui/game_ui.cpp
    src/ui/record_layer.cpp
    src/ui/render_settings_layer.cpp
    src/ui/load_macro_layer.cpp
    src/ui/clickbot_layer.cpp
    src/ui/button_setting.cpp
    src/practice_fixes/input.cpp
    src/practice_fixes/player.cpp
    src/practice_fixes/play_layer.cpp
)

add_library(${PROJECT_NAME} SHARED ${MOD_SOURCES})

# Configuración final obligatoria de Geode
setup_geode_mod(${PROJECT_NAME})
