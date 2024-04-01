project(vsc_vcpkg_demo VERSION 0.0.1 LANGUAGES CXX)

add_executable(vsc_vcpkg_demo
    # main.cc
    echo_server_with_as_tuple_default.cc
    boost_asio.cc
)

set_target_properties(vsc_vcpkg_demo
    PROPERTIES
        CXX_STANDARD 20
        CXX_EXTENSIONS ON
        CXX_STANDARD_REQUIRED ON
)

target_compile_options(vsc_vcpkg_demo
    PRIVATE
        -Wall -Wextra
)
target_compile_definitions(vsc_vcpkg_demo
    PRIVATE
)
target_link_options(vsc_vcpkg_demo
    PRIVATE
)
target_include_directories(vsc_vcpkg_demo
    PRIVATE
)

# Find libpcap library through pkg-config
# find_package(PkgConfig REQUIRED)
# pkg_check_modules(libpcap REQUIRED IMPORTED_TARGET libpcap)

# Find argparse library.
# find_package(argparse CONFIG REQUIRED)

# Find libfmt library.
find_package(fmt CONFIG REQUIRED)

# Find OpenSSL library(Boost.Asio depends on it).
find_package(OpenSSL REQUIRED)

# Find Boost library.
find_package(Boost REQUIRED context system)
target_compile_definitions(vsc_vcpkg_demo
    PRIVATE
        BOOST_USE_VALGRIND                 # Suppresses errors reported by valgrind
        BOOST_ASIO_DISABLE_BOOST_COROUTINE # Disable boost's coroutine used by ASIO before 1.80.0
        BOOST_ASIO_NO_DEPRECATED           # Disables Boost.Asio's deprecated interfaces and functionality
        BOOST_ASIO_SEPARATE_COMPILATION    # Separate compile Boost.Asio
)

set(CMAKE_THREAD_PREFER_PTHREAD TRUE)
set(THREADS_PREFER_PTHREAD_FLAG TRUE)
find_package(Threads REQUIRED)

target_link_libraries(vsc_vcpkg_demo
    PRIVATE
        # argparse::argparse
        # PkgConfig::libpcap
        fmt::fmt
        Boost::boost
        Boost::context
        Boost::system
        OpenSSL::SSL
        OpenSSL::Crypto
        Threads::Threads
)
