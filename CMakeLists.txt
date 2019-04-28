cmake_minimum_required(VERSION 3.0)
project(csv C)
include(GNUInstallDirs)
enable_testing()
#set(CMAKE_CTEST_COMMAND ctest -V)
set(CSV_VERSION_MAJOR 3)
set(CSV_VERSION_MINOR 3)
set(CSV_VERSION_PATCH 0)
set(CSV_VERSION_STRING ${CSV_VERSION_MAJOR}.${CSV_VERSION_MINOR}.${CSV_VERSION_PATCH} )

add_test(check_csv check_csv)
add_executable(check_csv test_csv.c)
target_link_libraries (check_csv LINK_PUBLIC csv)

add_library(csv libcsv.c csv.h) 
set_target_properties(csv PROPERTIES VERSION ${CSV_VERSION_STRING} SOVERSION ${CSV_VERSION_MAJOR} )

install(TARGETS csv
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}/static)
install(FILES csv.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(FILES csv.3 DESTINATION ${CMAKE_INSTALL_MANDIR})
