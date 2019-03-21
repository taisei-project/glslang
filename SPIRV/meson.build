
spirv_src = files(
    'GlslangToSpv.cpp',
    'InReadableOrder.cpp',
    'Logger.cpp',
    # 'SPVRemapper.cpp',  <-- don't want this one
    'SpvBuilder.cpp',
    'SpvPostProcess.cpp',
    'SpvTools.cpp',
    'disassemble.cpp',
    'doc.cpp',
)

libspirv = static_library('SPIRV',
    spirv_src,
    build_by_default : false,
    dependencies : spvtools_dep,
)
