if (ROS_GROOVY_OR_ABOVE_FOUND)
include(${CATKIN_DEVEL_PREFIX}/${CATKIN_PACKAGE_SHARE_DESTINATION}/cmake/test.cmake)
else()
include(${CMAKE_BINARY_DIR}/cmake/object_recognition_core/test.cmake)
endif()

# deal with the subdirectories as they contain macros
add_subdirectory(db)
add_subdirectory(share)

object_recognition_core_pytest(test_import)
object_recognition_core_pytest(test_config)

object_recognition_core_desktop_test(view_observations)

# check that at least the help completes correctly
object_recognition_core_help_test(${CMAKE_CURRENT_SOURCE_DIR}/../apps/detection)
object_recognition_core_help_test(${CMAKE_CURRENT_SOURCE_DIR}/../apps/training)

# check the different sources
object_recognition_core_source_test(OpenNI "object_recognition_core.io" "{}")

# check the different sinks
object_recognition_core_sink_test(GuessCsvWriter "object_recognition_core.io" "{}")

# check the constant pipeline
object_recognition_core_config_test(${CMAKE_CURRENT_SOURCE_DIR}/detection.test.ork)
