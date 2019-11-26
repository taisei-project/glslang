project('glslang', 'cpp',
    version : '7.13.3496',
    meson_version : '>=0.47.0',
    default_options : [
        'cpp_std=c++11',
    ]
)

cxx = meson.get_compiler('cpp')
add_project_arguments(cxx.get_supported_arguments('-fpermissive'), language : 'cpp')

threads_dep = dependency('threads')
spvtools_dep = dependency('SPIRV-Tools', required : get_option('enable_opt'), fallback : ['SPIRV-Tools', 'spirv_tools_opt_dep'])
spvtools_native_dep = dependency('SPIRV-Tools', required : false, native : true, fallback : ['SPIRV-Tools', 'spirv_tools_opt_native_dep'])

if not get_option('enable_hlsl').disabled()
    add_project_arguments('-DENABLE_HLSL', language : 'cpp')
endif

if spvtools_dep.found()
    add_project_arguments('-DENABLE_OPT=1', language : 'cpp')
else
    add_project_arguments('-DENABLE_OPT=0', language : 'cpp')

    if not get_option('enable_hlsl').disabled()
        message('SPIRV-Tools not linked - illegal SPIRV may be generated for HLSL')
    endif
endif

if host_machine.system() == 'windows'
    add_project_arguments('-DGLSLANG_OSINCLUDE_WIN32', language : 'cpp')
else
    add_project_arguments('-DGLSLANG_OSINCLUDE_UNIX', language : 'cpp')
endif

subdir('SPIRV')
subdir('OGLCompilersDLL')

if not get_option('enable_hlsl').disabled()
    subdir('hlsl')
endif

subdir('glslang')

glslang_dep = declare_dependency(
    link_with : libglslang,
    compile_args : glslang_args,  # because the google/khronos mouth breathers don't understand how public APIs work
    include_directories : include_directories('.'),
    version : meson.project_version(),
)

glslang_native_dep = declare_dependency(
    link_with : libglslang_native,
    compile_args : glslang_args,  # because the google/khronos mouth breathers don't understand how public APIs work
    include_directories : include_directories('.'),
    version : meson.project_version(),
)
