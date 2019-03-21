
liboglcompiler = static_library('OGLCompiler',
    'InitializeDll.cpp',
    dependencies : threads_dep,
    build_by_default : false,
)

liboglcompiler_native = static_library('OGLCompiler-native',
    'InitializeDll.cpp',
    dependencies : threads_native_dep,
    build_by_default : false,
    native : true,
    override_options : native_options,
)
