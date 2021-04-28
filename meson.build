project('glslang', 'cpp',
    version : '11.2.0',
    meson_version : '>=0.50.0',
    default_options : [
        'cpp_std=gnu++11',
    ]
)

native_options = [
    'b_lto=false',
    'b_ndebug=true',
    'b_sanitize=none',
    'debug=false',
    'optimization=0',
]

cxx = meson.get_compiler('cpp')
cxx_native = meson.get_compiler('cpp', native : true)

compiler_args = [
    '-fpermissive',
    '-fno-strict-aliasing',
]

add_project_arguments(cxx.get_supported_arguments(compiler_args), language : 'cpp', native : false)
add_project_arguments(cxx_native.get_supported_arguments(compiler_args), language : 'cpp', native : true)

project_args = []

threads_dep = dependency('threads')
threads_native_dep = dependency('threads', required : false, native : true)
spvtools_dep = dependency('SPIRV-Tools', required : get_option('enable_opt'), fallback : ['SPIRV-Tools', 'spirv_tools_opt_dep'])
spvtools_native_dep = dependency('SPIRV-Tools', required : false, native : true, fallback : ['SPIRV-Tools', 'spirv_tools_opt_native_dep'])

if not get_option('enable_hlsl').disabled()
    project_args += '-DENABLE_HLSL'
endif

if spvtools_dep.found()
    project_args += '-DENABLE_OPT=1'
else
    project_args += '-DENABLE_OPT=0'

    if not get_option('enable_hlsl').disabled()
        warning('SPIRV-Tools not linked - illegal SPIRV may be generated for HLSL')
    endif
endif

if host_machine.system() == 'windows'
    project_args += '-DGLSLANG_OSINCLUDE_WIN32'
else
    project_args += '-DGLSLANG_OSINCLUDE_UNIX'
endif

add_project_arguments(project_args, language : 'cpp', native : false)
add_project_arguments(project_args, language : 'cpp', native : true)

glslang_include_dirs = include_directories('.')

python = import('python').find_installation('python3').path()

subdir('glslang')
subdir('SPIRV')
subdir('OGLCompilersDLL')

glslang_libs = [libspirv, liboglcompiler]
glslang_native_libs = [libspirv_native, liboglcompiler_native]
glslang_args = []

if not get_option('enable_hlsl').disabled()
    glslang_libs += libhlsl
    glslang_native_libs += libhlsl_native
    glslang_args += '-DENABLE_HLSL'
endif

libglslang = library('glslang',
    glslang_src,
    cpp_pch : 'glslang/MachineIndependent/pch.h',
    link_with : glslang_libs,
    cpp_args : glslang_args,
    dependencies : [spvtools_dep, threads_dep],
    build_by_default : not meson.is_subproject(),
    include_directories : glslang_include_dirs,
)

libglslang_native = library('glslang-native',
    glslang_src,
    cpp_pch : 'glslang/MachineIndependent/pch.h',
    link_with : glslang_native_libs,
    cpp_args : glslang_args,
    dependencies : [spvtools_native_dep, threads_native_dep],
    build_by_default : false,
    native : true,
    include_directories : glslang_include_dirs,
    override_options : native_options,
)

glslang_dep = declare_dependency(
    link_with : libglslang,
    compile_args : glslang_args,  # because the google/khronos mouth breathers don't understand how public APIs work
    include_directories : glslang_include_dirs,
    version : meson.project_version(),
)

glslang_native_dep = declare_dependency(
    link_with : libglslang_native,
    compile_args : glslang_args,  # because the google/khronos mouth breathers don't understand how public APIs work
    include_directories : glslang_include_dirs,
    version : meson.project_version(),
)
