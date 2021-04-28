
build_info = custom_target('build_info.h',
    command : [
        python,
        files('../build_info.py'),
        meson.current_source_dir(),
        '-i', '@INTPUT@',
        '-o', '@OUTPUT@',
    ],
    depend_files : ['../CHANGES.md'],
    input : ['../build_info.h.tmpl'],
    output : ['build_info.h']
)

glslang_src = [build_info]

subdir('MachineIndependent')
subdir('GenericCodeGen')
subdir('OSDependent')
subdir('HLSL')

