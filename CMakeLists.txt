cmake_minimum_required(VERSION 2.8.8)
project(jbig2dec)

include_directories("${PROJECT_SOURCE_DIR}")
include_directories("${PROJECT_BINARY_DIR}")

set(obj "getopt1.c" "jbig2_arith.c" "jbig2_arith_int.c" "jbig2_generic.c" "jbig2_huffman.c" "jbig2_image_pbm.c" "jbig2_mmr.c" "jbig2_refinement.c" "jbig2_symbol_dict.c" "memcmp.c" "snprintf.c" "getopt.c" "jbig2_arith_iaid.c" "jbig2.c" "jbig2_halftone.c" "jbig2_image.c" "jbig2_metadata.c" "jbig2_page.c" "jbig2_segment.c" "jbig2_text.c" "sha1.c")
add_library(jbig2dec SHARED ${obj})
target_link_libraries(jbig2dec "dl")

add_definitions(-DHAVE_STDINT_H)

file (GLOB_RECURSE inc RELATIVE "${PROJECT_SOURCE_DIR}" "*.h")
# install binary
if (WIN32)
    install (FILES "${PROJECT_BINARY_DIR}/libjbig2dec.dll.a" DESTINATION lib)
    install (FILES "${PROJECT_BINARY_DIR}/libjbig2dec.dll" DESTINATION lib)
    install (FILES "${PROJECT_BINARY_DIR}/libjbig2dec.dll" DESTINATION bin)
else()
    install (TARGETS jbig2dec DESTINATION lib)
endif()
# install header
install (FILES ${inc} DESTINATION include/jbig2dec)
