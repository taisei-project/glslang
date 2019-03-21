
glslang_src = []

subdir('MachineIndependent')
subdir('GenericCodeGen')
subdir('OSDependent')

libglslang = library('glslang',
    glslang_src,
    cpp_pch : ['MachineIndependent/pch.h', 'MachineIndependent/pch.cpp'],
    link_with : [libspirv, liboglcompiler],
    dependencies : threads_dep,
    build_by_default : not meson.is_subproject(),
)
