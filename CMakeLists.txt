
cmake_minimum_required(VERSION 3.12)
project(varfile_krkrsdl2)

include(FetchContent)

FetchContent_Declare(
	krkrsdl2-ncbind
	GIT_REPOSITORY https://github.com/krkrsdl2/ncbind.git
	GIT_TAG origin/krkrsdl2
)

FetchContent_MakeAvailable(krkrsdl2-ncbind)

set(VARFILE_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR})
file(STRINGS ${VARFILE_SRC_DIR}/src_list/sources.txt VARFILE_SRC)
file(STRINGS ${VARFILE_SRC_DIR}/src_list/includes.txt VARFILE_INCLUDES)
list(TRANSFORM VARFILE_SRC PREPEND ${VARFILE_SRC_DIR}/)
list(TRANSFORM VARFILE_INCLUDES PREPEND ${VARFILE_SRC_DIR}/)

add_library(varfile MODULE)
set_target_properties(varfile PROPERTIES CXX_STANDARD 11)
set_target_properties(varfile PROPERTIES PREFIX "")
target_sources(varfile PRIVATE ${VARFILE_SRC})
target_include_directories(varfile PRIVATE ${VARFILE_INCLUDES})
target_link_libraries(varfile ncbind)
