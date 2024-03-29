# Reference:

#The name of the project
PROJECT(GPUDistTestSimple)

FIND_PACKAGE(CUDA)

#The CMake Minimum version that is required. The FindCUDA script
#is distributed since version 2.8
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

set(MYLIB_DIR 		"~/mylib" 	CACHE PATH "The path to MyLib.")	
set(3RDPARTY_DIR 	"~/lib" 	CACHE PATH "The path to 3rd party libraries.")	

include_directories(
	${MYLIB_DIR}/include		# MOD-BY-LEETEN 04/16/2012-FROM:	${MY_LIB_DIR}/include
	${3RDPARTY_DIR}/include	
	${CUDA_TOOLKIT_ROOT_DIR}/include
	${CUDA_SDK_ROOT_DIR}/common/inc
	../GPUDistLib/	# ADD-BY-LEETEN 03/19/2012
)

link_directories(
	${MYLIB_DIR}/lib		# MOD-BY-LEETEN 04/16/2012-FROM:	${MY_LIB_DIR}/lib
	${3RDPARTY_DIR}/lib
	${CUDA_TOOLKIT_ROOT_DIR}/lib/Win32
	${CUDA_SDK_ROOT_DIR}/common/lib/Win32
)

ADD_EXECUTABLE(${PROJECT_NAME}
	GPUDistTestSimple_main.cpp
)

# ADD-BY-LEETEN 01/28/2013-BEGIN
target_link_libraries(${PROJECT_NAME}
	GPUDistLib
	)
# ADD-BY-LEETEN 01/28/2013-END

# link OpenGL-related libraries
if(DEFINED WIN32)
	target_link_libraries(${PROJECT_NAME}
	)
else()
	target_link_libraries(${PROJECT_NAME}
	)
endif()

if(DEFINED WIN32)	# ADD-BY-LEETEN 09/02/2011
	target_link_libraries(${PROJECT_NAME}
		debug	libopt_d	optimized	libopt_r
		debug	lib3ds-120sd	optimized	lib3ds-120sd	# ADD-BY-LEETEN 04/17/2012
	)
# ADD-BY-LEETEN 09/02/2011-BEGIN
else()
	target_link_libraries(${PROJECT_NAME}
		libopt
		lib3ds-120s # ADD-BY-LEETEN 01/28/2013
	)
endif()

# # DEL-BY-LEETEN 01/28/2013-BEGIN
# target_link_libraries(${PROJECT_NAME}
# 	GPUDistLib
# 	)
# # DEL-BY-LEETEN 01/28/2013-END

# DEL-BY-LEETEN 04/17/2012-BEGIN
# # ADD-BY-LEETEN 04/13/2012-BEGIN
# target_link_libraries(${PROJECT_NAME}
	# lib3ds-120s
# )
# # ADD-BY-LEETEN 04/13/2012-END
# DEL-BY-LEETEN 04/17/2012-END

# ADD-BY-LEETEN 04/09/2012-BEGIN
install(
	TARGETS ${PROJECT_NAME}
	RUNTIME	DESTINATION bin
	ARCHIVE	DESTINATION	lib
	)	
# ADD-BY-LEETEN 04/09/2012-END
	
add_dependencies(GPUDistTestSimple GPUDistLib)	

#
# $Log$
#