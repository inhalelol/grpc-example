cmake_minimum_required(VERSION 3.5)

project(server-cpp LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Protobuf CONFIG REQUIRED)
find_package(gRPC CONFIG REQUIRED)

include_directories(${PROTOBUF_INCLUDE_DIRS} ${GRPC_INCLUDE_DIRS})
link_directories(${PROTOBUF_LIBRARY_DIRS} ${GRPC_LIBRARY_DIRS})

add_executable(server-cpp
    main.cpp
    service.pb.cc
    service.grpc.pb.cc
)

target_link_libraries(server-cpp gRPC::grpc++ protobuf::libprotobuf)

include(GNUInstallDirs)
install(TARGETS server-cpp
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
