project('glslang', 'cpp',
    version : '7.12.3352',
    meson_version : '>=0.45.0',
    default_options : [
        'cpp_std=c++11',
    ]
)

cxx = meson.get_compiler('cpp')
add_project_arguments(cxx.get_supported_arguments('-fpermissive'), language : 'cpp')

threads_dep = dependency('threads')

subdir('SPIRV')
subdir('OGLCompilersDLL')
subdir('glslang')

glslang_dep = declare_dependency(
    link_with : libglslang,
    include_directories : include_directories('.'),
)
