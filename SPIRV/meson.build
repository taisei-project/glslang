
spirv_src = files(
    'CInterface/spirv_c_interface.cpp',
    'disassemble.cpp',
    'doc.cpp',
    'GlslangToSpv.cpp',
    'InReadableOrder.cpp',
    'Logger.cpp',
    'SpvBuilder.cpp',
    'SpvPostProcess.cpp',
    # 'SPVRemapper.cpp',  <-- don't want this one
    'SpvTools.cpp',
)

libspirv = static_library('SPIRV',
    build_info, spirv_src,
    build_by_default : false,
    dependencies : spvtools_dep,
    include_directories : glslang_include_dirs,
    override_options : cross_options,
)

libspirv_native = static_library('SPIRV-native',
    build_info, spirv_src,
    build_by_default : false,
    dependencies : spvtools_native_dep,
    native : true,
    include_directories : glslang_include_dirs,
    override_options : native_options,
)
