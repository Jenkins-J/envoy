licenses(["notice"])  # Apache 2

cc_library(
    name = "crypto",
    srcs = [
        "crypto/libcrypto.a",
    ],
    hdrs = glob(["aws-lc/include/openssl/*.h"]),
    defines = ["BORINGSSL_FIPS"],
    includes = ["aws-lc/include"],
    visibility = ["//visibility:public"],
)

cc_library(
    name = "ssl",
    srcs = [
        "ssl/libssl.a",
    ],
    hdrs = glob(["aws-lc/include/openssl/*.h"]),
    includes = ["aws-lc/include"],
    visibility = ["//visibility:public"],
    deps = [":crypto"],
)

genrule(
    name = "build",
    srcs = glob(["aws-lc/**"]),
    outs = [
        "crypto/libcrypto.a",
        "ssl/libssl.a",
    ],
    cmd = "$(location {}) $(location crypto/libcrypto.a) $(location ssl/libssl.a)".format("@envoy//bazel/external:boringssl_fips.genrule_cmd"),
    tools = ["@envoy//bazel/external:boringssl_fips.genrule_cmd"],
)
