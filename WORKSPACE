"""Workspace file for lingvo."""

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load(
    "//lingvo:repo.bzl",
    "cc_tf_configure",
    "icu",
    "lingvo_protoc_deps",
    "lingvo_testonly_deps",
)

git_repository(
    name = "subpar",
    remote = "https://github.com/google/subpar",
    tag = "2.0.0",
)

git_repository(
    name = "cython",
    remote = "https://github.com/cython/cython",
    tag = "3.0a7",
)

# This is not robust. However, I don't know of a way to configure
# bazel to find the correct python. It appears that tensorflow and
# grpc have ways to do it, though.

new_local_repository(
    name = "python",
    path = "/install/miniconda3/envs/100k-hours-lingvo-3",
    build_file_content = """
cc_library(
    name = "python-lib",
    hdrs = glob(["include/python3.7m/*.h"]) +
           glob(["lib/python3.7/site-packages/numpy/core/include/numpy/*.h",
                 "lib/python3.7/site-packages/numpy/core/include/numpy/random/*.h"]),
    includes = ["include/python3.7m",
                "lib/python3.7/site-packages/numpy/core/include"],
    visibility = ["//visibility:public"]
)
    """
)

cc_tf_configure()

lingvo_testonly_deps()

lingvo_protoc_deps()

icu()