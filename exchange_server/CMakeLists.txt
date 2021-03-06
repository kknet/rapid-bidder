cmake_minimum_required(VERSION 3.1)

## Configuring to include framework
include_directories("${PROJECT_SOURCE_DIR}"
                    "${PROJECT_SOURCE_DIR}/framework/"
                    "${PROJECT_SOURCE_DIR}/framework/jsonv/include"
                   )

add_executable(
        multi_bidder_exchange_handler
        multi_bidder_exchange_handler.cpp
        )

if (WIN32)
    target_compile_definitions(multi_bidder_exchange_handler PRIVATE JSON_SO=1 _LIB JSON_COMPILING=1 _CRT_NONSTDC_NO_DEPRECATE )
    target_compile_definitions(jsonv PRIVATE JSON_SO=1 _LIB JSON_COMPILING=1)
endif(WIN32)

find_package (Threads)


if ( NOT WIN32)
set(RT_LIB rt)
endif(NOT WIN32)


target_link_libraries(
        multi_bidder_exchange_handler
        crud_service
        vanilla_rtb
        jsonv
        ${Boost_LIBRARIES}
        ${CMAKE_THREAD_LIBS_INIT}
        ${RT_LIB}
        )

install(TARGETS multi_bidder_exchange_handler
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
)


