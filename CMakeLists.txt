cmake_minimum_required(VERSION 3.22.1)
project(stock_app)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_BUILD_TYPE Debug)

set(Boost_ROOT "/home/nbaskey/my_opt/boost_libs")
find_package(Boost 1.84 REQUIRED COMPONENTS system thread)

set(cppzmq_DIR "/home/nbaskey/my_opt/cppzmq_libs/share/cmake/cppzmq")
find_package(cppzmq REQUIRED)
include_directories("/home/nbaskey/my_opt/cppzmq_libs/include")

add_executable(${CMAKE_PROJECT_NAME} 
        
    app/main.cpp

    src/match_engine_service.cpp
    src/order_book.cpp
    src/order.cpp
    src/trade.cpp
    src/stock_service.cpp
)

target_link_libraries(${CMAKE_PROJECT_NAME}
    PRIVATE ${Boost_SYSTEM_LIBRARY}
    PRIVATE ${Boost_THREAD_LIBRARY}
    PRIVATE cppzmq
)

target_include_directories(${CMAKE_PROJECT_NAME}
    PRIVATE ${Boost_INCLUDE_DIRS}
    PRIVATE include
)