
hlsl_src = files(
    'hlslAttributes.cpp',
    'hlslGrammar.cpp',
    'hlslOpMap.cpp',
    'hlslParseHelper.cpp',
    'hlslParseables.cpp',
    'hlslScanContext.cpp',
    'hlslTokenStream.cpp',
)

libhlsl = static_library('hlsl',
    hlsl_src,
    cpp_pch : 'meson-pch/pch.h',
    build_by_default : not meson.is_subproject(),
)
