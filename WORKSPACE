workspace(name = "com_github_bazel_test")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "new_git_repository")

http_archive(
    name = "rules_cc",
    sha256 = "eb389b5b74862a3d310ee9d6c63348388223b384ae4423ff0fd286fcd123942d",
    strip_prefix = "rules_cc-0.0.7",
    urls = ["https://github.com/bazelbuild/rules_cc/releases/download/0.0.7/rules_cc-0.0.7.tar.gz"],
)

# rules_foreign_cc
http_archive(
    name = "rules_foreign_cc",
    sha256 = "2a4d07cd64b0719b39a7c12218a3e507672b82a97b98c6a89d38565894cf7c51",
    strip_prefix = "rules_foreign_cc-0.9.0",
    url = "https://github.com/bazelbuild/rules_foreign_cc/archive/0.9.0.tar.gz",
)

load("@rules_foreign_cc//foreign_cc:repositories.bzl", "rules_foreign_cc_dependencies")

rules_foreign_cc_dependencies()

# http_archive(
#     name = "bazel_skylib",
#     sha256 = "3b620033ca48fcd6f5ef2ac85e0f6ec5639605fa2f627968490e52fc91a9932f",
#     strip_prefix = "bazel-skylib-1.3.0",
#     url = "https://github.com/bazelbuild/bazel-skylib/archive/refs/tags/1.3.0.tar.gz",
# )

# # Go
# http_archive(
#     name = "io_bazel_rules_go",
#     sha256 = "f74c98d6df55217a36859c74b460e774abc0410a47cc100d822be34d5f990f16",
#     urls = [
#         "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.47.1/rules_go-v0.47.1.zip",
#         "https://github.com/bazelbuild/rules_go/releases/download/v0.47.1/rules_go-v0.47.1.zip",
#     ],
# )

# load("@io_bazel_rules_go//go:deps.bzl", "go_download_sdk", "go_register_toolchains", "go_rules_dependencies")

# go_rules_dependencies()

# # Go - amd64/arm64
# GO_VERSION = "1.22.2"

# go_download_sdk(
#     name = "go_sdk_x86_64",
#     goarch = "amd64",
#     goos = "linux",
#     version = GO_VERSION,
# )

# go_download_sdk(
#     name = "go_sdk_arm64",
#     goarch = "arm64",
#     goos = "linux",
#     version = GO_VERSION,
# )

# go_download_sdk(
#     name = "go_sdk_darwin_arm64",
#     goarch = "arm64",
#     goos = "darwin",
#     version = GO_VERSION,
# )

# go_register_toolchains()

# load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

# bazel_skylib_workspace()

# load("@rules_cc//cc:repositories.bzl", "rules_cc_dependencies")

# rules_cc_dependencies()

http_archive(
    name = "assimp",
    build_file = "@//:third_party/assimp/build_file.bazel",
    sha256 = "a07666be71afe1ad4bc008c2336b7c688aca391271188eb9108d0c6db1be53f1",
    strip_prefix = "assimp-5.3.1",
    url = "https://github.com/assimp/assimp/archive/refs/tags/v5.3.1.tar.gz",
)

new_git_repository(
    name = "hpp-fcl",
    build_file = "@//:third_party/hpp-fcl/build_file.bazel",
    commit = "1c6f0a1d9c8d47914ab2196845327b3836de4b32",  # v2.4.4
    init_submodules = True,
    patch_args = ["-p1"],
    patches = ["@//:third_party/hpp-fcl/patches/cmake.patch"],
    remote = "https://github.com/humanoid-path-planner/hpp-fcl.git",
    # Remove this build directory, it causes issues on MacOS (see https://github.com/bazelbuild/bazel/issues/22484)
    # patch_cmds = ["rm -r third-parties/qhull/build"],
)

# http_archive(
#     name = "qhull",
#     build_file = "@//:third_party/qhull/build_file.bazel",
#     sha256 = "09e5e4c5b2b8a9e617a46876fef5a3d33e70aa1d08a163ff05d37701327c3be7",
#     strip_prefix = "qhull-8.1-alpha1",
#     url = "https://github.com/qhull/qhull/archive/refs/tags/v8.1-alpha1.tar.gz",
# )

http_archive(
    name = "folly",
    build_file = "@//:third_party/folly/build_file.bazel",
    sha256 = "f57f0d7726be7b0775fe717784e863866e207eff159b548a17f48d335d8e6504",
    url = "https://github.com/facebook/folly/releases/download/v2024.05.13.00/folly-v2024.05.13.00.tar.gz",
    # Remove this build directory, it causes issues on MacOS (see https://github.com/bazelbuild/bazel/issues/22484)
    # patch_cmds = ["rm -r folly/build"],
)

# LLVM toolchain - arm64
local_repository(
    name = "arm64_toolchain",
    path = "third_party/arm64_toolchain",
)

# LLVM toolchain
BAZEL_TOOLCHAIN_TAG = "0.8.2"

BAZEL_TOOLCHAIN_SHA = "3e251524b3e8f3b9ec93848e5267c168424f43b7b554efc983a5291c33d78cde"

http_archive(
    name = "com_grail_bazel_toolchain",
    canonical_id = BAZEL_TOOLCHAIN_TAG,
    sha256 = BAZEL_TOOLCHAIN_SHA,
    strip_prefix = "toolchains_llvm-{tag}".format(tag = BAZEL_TOOLCHAIN_TAG),
    url = "https://github.com/bazel-contrib/toolchains_llvm/archive/refs/tags/{tag}.tar.gz".format(tag = BAZEL_TOOLCHAIN_TAG),
)

load("@com_grail_bazel_toolchain//toolchain:deps.bzl", "bazel_toolchain_dependencies")

bazel_toolchain_dependencies()

load("@com_grail_bazel_toolchain//toolchain:rules.bzl", "llvm_toolchain")

llvm_toolchain(
    name = "llvm_toolchain",
    # TODO Find latest patch version for each platform and configure toolchain accordingly
    llvm_version = "14.0.0",
    stdlib = {
        "linux-x86_64": "stdc++",
        "linux-aarch64": "stdc++",
    },
)

load("@llvm_toolchain//:toolchains.bzl", "llvm_register_toolchains")

llvm_register_toolchains()
