
glslang_src = []

subdir('MachineIndependent')
subdir('GenericCodeGen')
subdir('OSDependent')

glslang_libs = [libspirv, liboglcompiler]
glslang_native_libs = [libspirv_native, liboglcompiler_native]
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

libglslang_native = library('glslang-native',
    glslang_src,
    cpp_pch : 'MachineIndependent/pch.h',
    link_with : glslang_native_libs,
    cpp_args : glslang_args,
    dependencies : [spvtools_native_dep, threads_dep],
    build_by_default : false,
    native : true,
)
