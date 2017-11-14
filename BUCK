include_defs('//BUCK_WINDOWS_COMMON')

unix_compiler_flags = ['-std=c++11']
macos_linker_flags = ['-framework', 'CoreFoundation',
        '-framework', 'Cocoa',
        '-framework', 'IOKit',
        '-framework', 'CoreVideo']

prebuilt_cxx_library(
    name = 'glfw',
    platform_static_lib = [
        ('^windows.*', 'glfw/windows/lib-vs2015/glfw3.lib'),
        ('^macos.*', 'glfw/macos/lib/libglfw3.a'),
        # Comment out the below line to build
        ('^linux.*', 'glfw/linux/lib/libglfw3.so')
    ],
    exported_platform_headers = [
        ('^windows.*', subdir_glob([('glfw/windows/include/GLFW', '**/*.h')])),
        ('^macos.*', subdir_glob([('glfw/macos/include/GLFW', '**/*.h')])),
        # Comment out the below line to build
        ('^linux.*', subdir_glob([('glfw/linux/include/GLFW', '**/*.h')]))
    ],
    preferred_linkage = 'static',
    header_namespace = 'GLFW',
    visibility = [
        'PUBLIC'
    ]
)

cxx_binary(
    name = 'ex',
    srcs = glob([
        'src/**/*.cpp'
    ]),
    headers = subdir_glob([
        ('include', '**/*.hpp')
    ]),
    platform_compiler_flags = [
        ('^macos.*', unix_compiler_flags), #macosx-x86_64
        ('^windows.*', WINDOWS_COMPILE_FLAGS) #windows-x86_64
    ],
    platform_linker_flags = [
        ('^macos.*', macos_linker_flags), #macosx-x86_64
        ('^windows.*', WINDOWS_LINKER_FLAGS + WINDOWS_COMMON_LIB + ['opengl32.lib']) #windows-x86_64
    ],
    header_namespace = 'ex',
    deps = [
        '//:glfw'
    ]
)