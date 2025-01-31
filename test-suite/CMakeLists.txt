set(QLXAD_TEST_SOURCES
    americanoption_xad.cpp
    batesmodel_xad.cpp
    quantlibtestsuite_xad.cpp
    utilities_xad.cpp
)

set(QLXAD_TEST_HEADERS
    americanoption_xad.hpp
    batesmodel_xad.hpp
    utilities_xad.hpp
)

if(QL_BUILD_TEST_SUITE)
    add_executable(qlxad_test_suite ${QLXAD_TEST_SOURCES} ${QLXAD_TEST_HEADERS})
    set_target_properties(qlxad_test_suite PROPERTIES OUTPUT_NAME "quantlib-xad-test-suite")
    if (NOT Boost_USE_STATIC_LIBS)
        target_compile_definitions(qlxad_test_suite PRIVATE BOOST_ALL_DYN_LINK BOOST_TEST_DYN_LINK)
    endif()
    target_link_libraries(qlxad_test_suite PRIVATE
        ql_library
        ql_unit_test_main
        ${QL_THREAD_LIBRARIES})
    if (QL_INSTALL_TEST_SUITE)
        install(TARGETS qlxad_test_suite RUNTIME DESTINATION ${QL_INSTALL_BINDIR})
    endif()
    add_test(NAME quantlib_xad_test_suite COMMAND qlxad_test_suite --log_level=message)
endif()