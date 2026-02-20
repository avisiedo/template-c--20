
find_package(GTest REQUIRED)


add_executable(my_app_main_test
    main_test.cpp
)


target_link_libraries(my_app_main_test
    PRIVATE
        GTest::GTest
        GTest::Main
)

include(GoogleTest)
gtest_discover_tests(my_app_main_test)

