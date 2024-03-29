add_executable (dynanode
	daemon.cpp
	daemon.hpp
	entry.cpp)

target_link_libraries (dynanode
	node
	secure
	argon2
	Boost::boost
	${PLATFORM_LIBS}
)

target_compile_definitions(dynanode
	PRIVATE
		-DNANO_VERSION_MAJOR=${CPACK_PACKAGE_VERSION_MAJOR}
		-DNANO_VERSION_MINOR=${CPACK_PACKAGE_VERSION_MINOR}
		-DNANO_VERSION_PATCH=${CPACK_PACKAGE_VERSION_PATCH})

set_target_properties (dynanode
	PROPERTIES
		COMPILE_FLAGS
			"-DQT_NO_KEYWORDS -DBOOST_ASIO_HAS_STD_ARRAY=1")

if ((NANO_GUI OR RAIBLOCKS_GUI) AND NOT APPLE)
	install(TARGETS dynanode
			RUNTIME DESTINATION bin
			LIBRARY DESTINATION lib
			ARCHIVE DESTINATION lib
	)
endif()
