load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "imgui-1.91.8",
    build_file_content = """
cc_library(
    name = "imgui-1.91.8",
    srcs = [
        "backends/imgui_impl_glfw.cpp",
        "backends/imgui_impl_opengl3.cpp",
        "imgui.cpp",
        "imgui_demo.cpp",
        "imgui_draw.cpp",
        "imgui_tables.cpp",
        "imgui_widgets.cpp",
    ],
    hdrs = [
        "backends/imgui_impl_glfw.h",
        "backends/imgui_impl_opengl3.h",
        "backends/imgui_impl_opengl3_loader.h",
        "imconfig.h",
        "imgui.h",
        "imgui_internal.h",
        "imstb_rectpack.h",
        "imstb_textedit.h",
        "imstb_truetype.h",
    ],
    deps = [
        "@glfw-3.3.9",
    ],
    linkopts = ["-ldl"],
    includes = ["."],
    include_prefix = "imgui",
    visibility = ["//visibility:public"],
)
""",
    strip_prefix = "imgui-1.91.8",
    urls = ["https://github.com/ocornut/imgui/archive/refs/tags/v1.91.8.tar.gz"],
)

http_archive(
    name = "glfw-3.3.9",
    build_file_content = """
cc_library(
    name = "glfw-headers",
    hdrs = [
        "include/GLFW/glfw3.h",
        "include/GLFW/glfw3native.h",
    ],
    strip_include_prefix = "include",
    includes = ['.'],
    visibility = [
        "//visibility:private",
    ],
)
DARWIN_HDRS = [
    "src/cocoa_joystick.h",
    "src/cocoa_platform.h",
    "src/glx_context.h",
    "src/nsgl_context.h",
    "src/null_joystick.h",
    "src/null_platform.h",
    "src/posix_thread.h",
    "src/wl_platform.h",
]

DARWIN_SRCS = [
    "src/cocoa_time.c",
    "src/posix_thread.c",
    "src/cocoa_init.m",
    "src/cocoa_joystick.m",
    "src/cocoa_monitor.m",
    "src/cocoa_window.m",
    "src/nsgl_context.m",
]

COMMON_HDRS = [
    "include/GLFW/glfw3.h",
    "include/GLFW/glfw3native.h",
    "src/egl_context.h",
    "src/internal.h",
    "src/osmesa_context.h",
    "src/mappings.h",
    "src/xkb_unicode.h",
]

COMMON_SRCS = [
    "src/context.c",
    "src/egl_context.c",
    "src/init.c",
    "src/input.c",
    "src/osmesa_context.c",
    "src/monitor.c",
    "src/vulkan.c",
    "src/window.c",
    "src/xkb_unicode.c",
]

DARWIN_LINKOPTS = [
    "-framework OpenGL",
    "-framework Cocoa",
    "-framework IOKit",
    "-framework CoreFoundation",
]

LINUX_HDRS = [
    "src/glx_context.h",
    "src/linux_joystick.h",
    "src/posix_thread.h",
    "src/posix_time.h",
    "src/x11_platform.h",
]

LINUX_SRCS = [
    "src/glx_context.c",
    "src/linux_joystick.c",
    "src/posix_thread.c",
    "src/posix_time.c",
    "src/x11_init.c",
    "src/x11_monitor.c",
    "src/x11_window.c",
]

objc_library( # For the Objective-C parts
    name = "glfw-cocoa",
    srcs = COMMON_SRCS + DARWIN_SRCS,
    hdrs = COMMON_HDRS + DARWIN_HDRS,
    copts = [
        "-fno-objc-arc",
    ],
    defines = ["_GLFW_COCOA", "GLFW_INVALID_CODEPOINT"],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "glfw-linux",
    srcs = COMMON_SRCS + LINUX_SRCS,
    hdrs = COMMON_HDRS + LINUX_HDRS,
    visibility = ["//visibility:public"],
    defines = ["_GLFW_X11"],
    linkopts = ["-lX11"],
)

cc_library(
    name = "glfw-3.3.9",
    deps = select({
        "@bazel_tools//src/conditions:linux_x86_64": [":glfw-headers", ":glfw-linux"],
        "@bazel_tools//src/conditions:darwin": [":glfw-headers", ":glfw-cocoa"]
    }),
    linkopts = select({
        "@bazel_tools//src/conditions:linux_x86_64": [],
        "@bazel_tools//src/conditions:darwin": DARWIN_LINKOPTS,
    }),
    visibility = ["//visibility:public"],
)
""",
    sha256 = "a7e7faef424fcb5f83d8faecf9d697a338da7f7a906fc1afbc0e1879ef31bd53",
    strip_prefix = "glfw-3.3.9",
    urls = ["https://github.com/glfw/glfw/archive/refs/tags/3.3.9.tar.gz"],
)

http_archive(
    name = "implot-0.16",
    build_file_content = """
cc_library(
    name = "implot-0.16",
    srcs = ["implot.cpp", "implot_items.cpp", "implot_demo.cpp"],
    hdrs = ["implot.h", "implot_internal.h"],
    deps = [
        "@imgui-1.91.8",
    ],
    visibility = ["//visibility:public"], 
)
""",
    strip_prefix = "implot-0.16",
    urls = ["https://github.com/epezent/implot/archive/refs/tags/v0.16.tar.gz"],
)
