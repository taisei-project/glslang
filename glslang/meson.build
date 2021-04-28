
build_info = custom_target('build_info.h',
    command : [
        python,
        glslang_buildinfo_gen,
        glslang_source_root,
        '-i', '@INPUT@',
        '-o', '@OUTPUT@',
    ],
    depend_files : [glslang_changes],
    input : [glslang_buildinfo_tmpl],
    output : ['build_info.h']
)

glslang_src = [build_info]

subdir('MachineIndependent')
subdir('GenericCodeGen')
subdir('OSDependent')
subdir('HLSL')

