load("//tensorflow:tensorflow.bzl", "filegroup")
load("//tensorflow/compiler/mlir:glob_lit_test.bzl", "glob_lit_tests")
load("//tensorflow:tensorflow.bzl", "tf_cc_test")
load(
    "//tensorflow/core/platform:build_config_root.bzl",
    "tf_cuda_tests_tags",
)

package(licenses = ["notice"])

glob_lit_tests(
    data = [":test_utilities"],
    driver = "@llvm-project//mlir:run_lit.sh",
    tags_override = {
        "hlo_to_lhlo_with_xla/gpu_ops.mlir": tf_cuda_tests_tags(),
    },
    test_file_exts = [
        "mlir",
        "hlotxt",
    ],
)

# Bundle together all of the test utilities that are used by tests.
filegroup(
    name = "test_utilities",
    testonly = True,
    data = [
        "//tensorflow/compiler/mlir:tf-mlir-translate",
        "//tensorflow/compiler/mlir:tf-opt",
        "//tensorflow/compiler/mlir/xla:xla-opt",
        "@llvm-project//llvm:FileCheck",
    ],
)

tf_cc_test(
    name = "mlir_hlo_builder_test",
    srcs = ["mlir_hlo_builder_test.cc"],
    deps = [
        "//tensorflow/compiler/mlir/hlo",
        "//tensorflow/compiler/mlir/xla:mlir_hlo_builder",
        "//tensorflow/compiler/xla:shape_util",
        "//tensorflow/core:test",
        "//tensorflow/core:test_main",
        "//tensorflow/core:testlib",
        "@llvm-project//llvm:Support",
        "@llvm-project//mlir:IR",
    ],
)
