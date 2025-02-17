exports_files(["LICENSE"])

cc_library(
    name = "include",
    hdrs = glob([
        "include/**/*.h",
        "include/**/*.hpp",
    ]),
    includes = ["include"],
    strip_include_prefix = "include",
)

_COMPUTE_LIBRARY_DEFINES = [
    "ARM_COMPUTE_CPP_SCHEDULER",
    "ARM_COMPUTE_CPU_ENABLED",
    "ENABLE_NEON",
    "ARM_COMPUTE_ENABLE_NEON",
    "ENABLE_SVE",
    "ARM_COMPUTE_ENABLE_SVE",
    "ARM_COMPUTE_ENABLE_FP16",
    "ARM_COMPUTE_ENABLE_BF16",
    "ARM_COMPUTE_ENABLE_I8MM",
    "ARM_COMPUTE_ENABLE_SVEF32MM",
    "ENABLE_FP16_KERNELS",
    "ENABLE_FP32_KERNELS",
    "ENABLE_QASYMM8_KERNELS",
    "ENABLE_QASYMM8_SIGNED_KERNELS",
    "ENABLE_QSYMM16_KERNELS",
    "ENABLE_INTEGER_KERNELS",
    "ENABLE_NHWC_KERNELS",
]

cc_library(
    name = "arm_compute_sve",
    srcs = glob(
        [
            "src/core/NEON/kernels/arm_gemm/kernels/sve_*/*.cpp",
            "src/core/NEON/kernels/arm_conv/**/kernels/sve_*/*.cpp",
            "src/core/NEON/kernels/arm_conv/depthwise/interleaves/sve_*.cpp",
            "src/core/cpu/kernels/**/sve/*.cpp",
            "**/*.h",
        ],
    ) + [
        "src/core/NEON/kernels/arm_gemm/transform-sve.cpp",
        "src/core/NEON/kernels/arm_gemm/mergeresults-sve.cpp",
        "src/core/NEON/kernels/batchnormalization/impl/SVE/fp16.cpp",
        "src/core/NEON/kernels/batchnormalization/impl/SVE/fp32.cpp",
    ],
    hdrs = glob([
        "arm_compute/runtime/**/*.h",
        "arm_compute/runtime/*.h",
        "arm_compute/core/**/*.h",
        "**/*.inl",
    ]) + [
        "arm_compute_version.embed",
    ],
    copts = ["-march=armv8.2-a+sve"],
    defines = _COMPUTE_LIBRARY_DEFINES,
    includes = [
        "src/core/NEON/kernels/arm_gemm",
        "src/core/NEON/kernels/assembly",
        "src/core/cpu/kernels/assembly",
    ],
    linkopts = ["-lpthread"],
    deps = ["include"],
)

cc_library(
    name = "arm_compute",
    srcs = glob(
        [
            "src/common/**/*.cpp",
            "src/core/*.cpp",
            "src/core/CPP/kernels/*.cpp",
            "src/core/helpers/*.cpp",
            "src/core/utils/**/*.cpp",
            "src/runtime/**/*.cpp",
            "src/c/*.cpp",
            "src/cpu/*.cpp",
            "src/core/NEON/kernels/*.cpp",
            "src/core/NEON/kernels/arm_gemm/kernels/a64_*/*.cpp",
            "src/core/NEON/kernels/arm_conv/**/kernels/a64_*/*.cpp",
            "src/core/NEON/kernels/convolution/**/*.cpp",
            "src/core/NEON/kernels/arm_conv/depthwise/interleaves/a64_*.cpp",
            "src/core/cpu/kernels/*.cpp",
            "src/core/cpu/kernels/**/neon/*.cpp",
            "src/core/NEON/kernels/arm_gemm/*.cpp",
            "**/*.h",
        ],
        exclude = [
            "src/core/utils/logging/**",
            "src/core/TracePoint.cpp",
            "src/core/NEON/kernels/arm_gemm/mergeresults-sve.cpp",
            "src/core/NEON/kernels/arm_gemm/transform-sve.cpp",
            "src/runtime/CL/**",
            "src/runtime/gpu/**",
        ],
    ) + [
        "src/core/CPP/CPPTypes.cpp",
        "src/c/operators/AclActivation.cpp",
        "src/core/NEON/kernels/arm_conv/pooling/kernels/cpp_nhwc_1x1_stride_any_depthfirst/generic.cpp",
        "src/core/NEON/kernels/arm_conv/depthwise/interleaves/8b_mla.cpp",
        "src/core/NEON/kernels/batchnormalization/impl/NEON/fp16.cpp",
        "src/core/NEON/kernels/batchnormalization/impl/NEON/fp32.cpp",
    ],
    hdrs = glob([
        "src/core/NEON/kernels/**/*.h",
        "src/core/NEON/kernels/**/*.hpp",
        "arm_compute/runtime/**/*.h",
        "arm_compute/runtime/*.h",
        "arm_compute/core/**/*.h",
        "**/*.inl",
    ]) + [
        "arm_compute_version.embed",
    ],
    defines = _COMPUTE_LIBRARY_DEFINES,
    includes = [
        "arm_compute/runtime",
        "src/core/NEON/kernels/assembly",
        "src/core/NEON/kernels/convolution/common",
        "src/core/NEON/kernels/convolution/winograd",
        "src/core/cpu/kernels/assembly",
    ],
    linkopts = ["-lpthread"],
    visibility = ["//visibility:public"],
    deps = [
        "arm_compute_sve",
        "include",
    ],
)
