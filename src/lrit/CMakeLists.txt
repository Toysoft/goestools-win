find_package(nlohmann_json CONFIG REQUIRED)
add_library(lrit lrit.cc file.cc json.cc)
target_link_libraries(lrit util nlohmann_json::nlohmann_json)

add_executable(lritdump lritdump.cc)
find_library(GETOPT_LIB getopt)
add_sanitizers(lritdump)
target_link_libraries(lritdump lrit ${GETOPT_LIB})
set_target_properties(lritdump PROPERTIES LINK_FLAGS "setargv.obj")

add_executable(areadump areadump.cc)
add_sanitizers(areadump)
target_link_libraries(areadump lrit dir shlwapi)
set_target_properties(areadump PROPERTIES LINK_FLAGS "setargv.obj")
