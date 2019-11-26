
glslang_src = []

subdir('MachineIndependent')
subdir('GenericCodeGen')
subdir('OSDependent')

glslang_libs = [libspirv, liboglcompiler]
glslang_args = []

if not get_option('enable_hlsl').disabled()
    glslang_libs += libhlsl
    glslang_args += '-DENABLE_HLSL'
endif

libglslang = library('glslang',
    glslang_src,
    cpp_pch : 'MachineIndependent/pch.h',
    link_with : glslang_libs,
    cpp_args : glslang_args,
    dependencies : [spvtools_dep, threads_dep],
    build_by_default : not meson.is_subproject(),
)
