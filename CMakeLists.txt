# CMakeList.txt : projet CMake pour RR-GraphCut, incluez la source et définissez
# la logique spécifique au projet ici.
#
cmake_minimum_required (VERSION 3.8)

# Activez Rechargement à chaud pour les compilateurs MSVC si cela est pris en charge.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("RR-GraphCut")

find_package(ZLIB REQUIRED)
find_package(PNG REQUIRED)

# Ajoutez une source à l'exécutable de ce projet.
add_executable (RR-GraphCut "RR-GraphCut.cpp" "RR-GraphCut.h" "io_png.c" "io_png.h" "maxflow/graph.cpp")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET RR-GraphCut PROPERTY CXX_STANDARD 20)
endif()

# TODO: Ajoutez des tests et installez des cibles si nécessaire.
target_link_libraries(RR-GraphCut PRIVATE PNG::PNG)
target_link_libraries(RR-GraphCut PRIVATE ZLIB::ZLIB)