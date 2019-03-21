
glslang_src = []

subdir('MachineIndependent')
subdir('GenericCodeGen')
subdir('OSDependent')

glslang_libs = [libspirv, liboglcompiler]

if not get_option('enable_hlsl').disabled()
    glslang_libs += libhlsl
endif

libglslang = library('glslang',
    glslang_src,
    cpp_pch : 'MachineIndependent/pch.h',
    link_with : glslang_libs,
    dependencies : [spvtools_dep, threads_dep],
    build_by_default : not meson.is_subproject(),
)
