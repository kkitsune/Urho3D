cmake_minimum_required(VERSION 3.2 FATAL_ERROR)
project(Urho3D)

set(CXX_STANDARD_REQUIRED on)
set(CMAKE_CXX_STANDARD 14)

include(GenerateExportHeader)
include(ExternalProject)

include(compile-options.cmake)

# Set runtime path
set(CMAKE_SKIP_BUILD_RPATH            FALSE) # Add absolute path to all dependencies for BUILD
set(CMAKE_BUILD_WITH_INSTALL_RPATH    FALSE) # Use CMAKE_INSTALL_RPATH for INSTALL
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH FALSE) # Do NOT add path to dependencies for INSTALL

cmake_policy(SET CMP0004 OLD)

add_library(Urho3D SHARED
		include/Urho3D/DebugNew.h
		source/Precompiled.h

		include/Urho3D/Container/Allocator.h
		include/Urho3D/Container/ArrayPtr.h
		include/Urho3D/Container/ForEach.h
		include/Urho3D/Container/Hash.h
		include/Urho3D/Container/HashBase.h
		include/Urho3D/Container/HashMap.h
		include/Urho3D/Container/HashSet.h
		include/Urho3D/Container/LinkedList.h
		include/Urho3D/Container/List.h
		include/Urho3D/Container/ListBase.h
		include/Urho3D/Container/Pair.h
		include/Urho3D/Container/Ptr.h
		include/Urho3D/Container/RefCounted.h
		include/Urho3D/Container/Sort.h
		include/Urho3D/Container/Str.h
		include/Urho3D/Container/Swap.h
		include/Urho3D/Container/Vector.h
		include/Urho3D/Container/VectorBase.h
		source/Container/Allocator.cpp
		source/Container/HashBase.cpp
		source/Container/RefCounted.cpp
		source/Container/Str.cpp
		source/Container/Swap.cpp
		source/Container/VectorBase.cpp

		include/Urho3D/Core/Attribute.h
		include/Urho3D/Core/Condition.h
		include/Urho3D/Core/Context.h
		include/Urho3D/Core/CoreEvents.h
		include/Urho3D/Core/EventProfiler.h
		include/Urho3D/Core/Main.h
		include/Urho3D/Core/MiniDump.h
		include/Urho3D/Core/Mutex.h
		include/Urho3D/Core/Object.h
		include/Urho3D/Core/ProcessUtils.h
		include/Urho3D/Core/Profiler.h
		include/Urho3D/Core/Spline.h
		include/Urho3D/Core/StringUtils.h
		include/Urho3D/Core/Thread.h
		include/Urho3D/Core/Timer.h
		include/Urho3D/Core/Variant.h
		include/Urho3D/Core/WorkQueue.h
		source/Core/Condition.cpp
		source/Core/Context.cpp
		source/Core/EventProfiler.cpp
		source/Core/MiniDump.cpp
		source/Core/Mutex.cpp
		source/Core/Object.cpp
		source/Core/ProcessUtils.cpp
		source/Core/Profiler.cpp
		source/Core/Spline.cpp
		source/Core/StringUtils.cpp
		source/Core/Thread.cpp
		source/Core/Timer.cpp
		source/Core/Variant.cpp
		source/Core/WorkQueue.cpp

		include/Urho3D/IO/Compression.h
		include/Urho3D/IO/Deserializer.h
		include/Urho3D/IO/File.h
		include/Urho3D/IO/FileSystem.h
		include/Urho3D/IO/FileWatcher.h
		include/Urho3D/IO/IOEvents.h
		include/Urho3D/IO/Log.h
		include/Urho3D/IO/MacFileWatcher.h
		include/Urho3D/IO/MemoryBuffer.h
		include/Urho3D/IO/NamedPipe.h
		include/Urho3D/IO/PackageFile.h
		include/Urho3D/IO/RWOpsWrapper.h
		include/Urho3D/IO/Serializer.h
		include/Urho3D/IO/VectorBuffer.h
		source/IO/Compression.cpp
		source/IO/Deserializer.cpp
		source/IO/File.cpp
		source/IO/FileSystem.cpp
		source/IO/FileWatcher.cpp
		source/IO/Log.cpp
		#source/IO/MacFileWatcher.m
		source/IO/MemoryBuffer.cpp
		source/IO/NamedPipe.cpp
		source/IO/PackageFile.cpp
		source/IO/Serializer.cpp
		source/IO/VectorBuffer.cpp

		include/Urho3D/Math/AreaAllocator.h
		include/Urho3D/Math/BoundingBox.h
		include/Urho3D/Math/Color.h
		include/Urho3D/Math/Frustum.h
		include/Urho3D/Math/MathDefs.h
		include/Urho3D/Math/Matrix2.h
		include/Urho3D/Math/Matrix3.h
		include/Urho3D/Math/Matrix3x4.h
		include/Urho3D/Math/Matrix4.h
		include/Urho3D/Math/Plane.h
		include/Urho3D/Math/Polyhedron.h
		include/Urho3D/Math/Quaternion.h
		include/Urho3D/Math/Random.h
		include/Urho3D/Math/Ray.h
		include/Urho3D/Math/Rect.h
		include/Urho3D/Math/Sphere.h
		include/Urho3D/Math/StringHash.h
		include/Urho3D/Math/Vector2.h
		include/Urho3D/Math/Vector3.h
		include/Urho3D/Math/Vector4.h
		source/Math/AreaAllocator.cpp
		source/Math/BoundingBox.cpp
		source/Math/Color.cpp
		source/Math/Frustum.cpp
		source/Math/MathDefs.cpp
		source/Math/Matrix2.cpp
		source/Math/Matrix3.cpp
		source/Math/Matrix3x4.cpp
		source/Math/Matrix4.cpp
		source/Math/Plane.cpp
		source/Math/Polyhedron.cpp
		source/Math/Quaternion.cpp
		source/Math/Random.cpp
		source/Math/Ray.cpp
		source/Math/Rect.cpp
		source/Math/Sphere.cpp
		source/Math/StringHash.cpp
		source/Math/Vector2.cpp
		source/Math/Vector3.cpp
		source/Math/Vector4.cpp)

target_include_directories(Urho3D PUBLIC
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
		$<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/include>
		$<INSTALL_INTERFACE:include>
		PRIVATE source)

export(TARGETS Urho3D FILE Urho3DConfig.cmake)
generate_export_header(Urho3D
		EXPORT_FILE_NAME  include/Urho3D/config.h
		EXPORT_MACRO_NAME URHO3D_API)

target_compile_options(Urho3D
		PRIVATE ${DEFAULT_COMPILE_OPTIONS})

target_compile_definitions(Urho3D
		PRIVATE ${DEFAULT_COMPILE_DEFINITIONS} Urho3D_EXPORTS
		PUBLIC)

find_package(OpenGL REQUIRED)

target_link_libraries(Urho3D ${DEFAULT_LINKER_OPTIONS}
		${Boost_LIBRARIES} ${OPENGL_LIBRARIES})

install(TARGETS Urho3D
		ARCHIVE  DESTINATION lib
		LIBRARY  DESTINATION lib
		RUNTIME  DESTINATION bin)
install(DIRECTORY include/ DESTINATION include)
