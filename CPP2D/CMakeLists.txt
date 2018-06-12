cmake_minimum_required(VERSION 3.5)

project(cpp2d)

# Déclaration de l'exécutable
add_executable(
    cpp2d
    CPP2D.cpp
    CPP2DConsumer.cpp
    CPP2DFrontendAction.cpp
    CPP2DPPHandling.cpp
    CPP2DTools.cpp
    DPrinter.cpp
    MatchContainer.cpp
    CustomPrinters.cpp
	Options.cpp
    CustomPrinters/boost_port.cpp
    CustomPrinters/c_stdlib_port.cpp
    CustomPrinters/cpp_stdlib_port.cpp
)

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})

llvm_map_components_to_libnames(llvm_libs
  X86AsmParser # MC, MCParser, Support, X86Desc, X86Info
  X86Desc # MC, Support, X86AsmPrinter, X86Info
  X86AsmPrinter # MC, Support, X86Utils
  X86Info # MC, Support, Target
  X86Utils # Core, Support
  ipo
  ScalarOpts
  InstCombine
  TransformUtils
  Analysis
  Target
  Option # Support
  MCParser # MC, Support
  MC # Object, Support
  Object # BitReader, Core, Support
  BitReader # Core, Support
  Core # Support
  ProfileData
  Support
)

if(CMAKE_COMPILER_IS_GNUCXX)
    SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti")
    target_link_libraries(cpp2d rt dl tinfo pthread z m)
endif()

if(CMAKE_SYSTEM_NAME MATCHES "Windows")
	target_link_libraries(cpp2d
		version.lib
	)
endif()
