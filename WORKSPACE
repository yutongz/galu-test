workspace(name = "com_github_google_galu")

git_repository(
    name = "bazel_skylib",
    commit = "2169ae1c374aab4a09aa90e65efe1a3aad4e279b",
    remote = "https://github.com/bazelbuild/bazel-skylib.git",
)

load("@bazel_skylib//:lib.bzl", "versions")

http_archive(
    name = "io_bazel_rules_go",
    url = "https://github.com/bazelbuild/rules_go/releases/download/0.10.3/rules_go-0.10.3.tar.gz",
    sha256 = "feba3278c13cde8d67e341a837f69a029f698d7a27ddbb2a202be7a10b22142a",
)

http_archive(
    name = "bazel_gazelle",
    url = "https://github.com/bazelbuild/bazel-gazelle/releases/download/0.10.1/bazel-gazelle-0.10.1.tar.gz",
    sha256 = "d03625db67e9fb0905bbd206fa97e32ae9da894fe234a493e7517fd25faec914",
)

http_archive(
    name = "com_google_protobuf",
    sha256 = "cef7f1b5a7c5fba672bec2a319246e8feba471f04dcebfe362d55930ee7c1c30",
    strip_prefix = "protobuf-3.5.0",
    urls = ["https://github.com/google/protobuf/archive/v3.5.0.zip"],
)



bind(
    name = "protoc",
    actual = "@com_github_google_protobuf//:protoc",
)

load("@io_bazel_rules_go//go:def.bzl","go_rules_dependencies","go_repository","go_register_toolchains",)

go_rules_dependencies()
go_register_toolchains(go_version = "1.10")

load("@io_bazel_rules_go//proto:def.bzl", "proto_register_toolchains")
load("@io_bazel_rules_go//go:def.bzl", "go_repositories", "new_go_repository", "go_repository")


load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
gazelle_dependencies()


GOOGLEAPIS_BUILD_FILE = """
load("@io_bazel_rules_go//proto:def.bzl", "go_proto_library")
package(default_visibility = ["//visibility:public"])
proto_library(
    name = "api_proto",
    srcs = [
          "google/api/annotations.proto",
          "google/api/http.proto",
    ],
    deps = [
          "@com_google_protobuf//:descriptor_proto",
    ],
)

go_proto_library(
    name = "api_go_proto",
    importpath = "google/api",
    proto = ":api_proto",
    deps = [
        "@com_github_golang_protobuf//protoc-gen-go/descriptor:go_default_library",
    ],
)
"""

new_git_repository(
    name = "com_github_googleapis_googleapis",
    build_file_content = GOOGLEAPIS_BUILD_FILE,
    commit = "13ac2436c5e3d568bd0e938f6ed58b77a48aba15",  # Oct 21, 2016 (only release pre-dates sha)
    remote = "https://github.com/googleapis/googleapis.git",
)

go_repository(
  name = "com_github_google_go_genproto",
  commit = "7fd901a49ba6a7f87732eb344f6e3c5b19d1b200",
  importpath = "github.com/google/go-genproto",
)

go_repository(
  name = "com_github_golang_protobuf",
  commit = "925541529c1fa6821df4e44ce2723319eb2be768",
  importpath = "github.com/golang/protobuf",
)

go_repository(
    name = "org_golang_google_genproto",
    commit = "aa2eb687b4d3e17154372564ad8d6bf11c3cf21f",  # June 1, 2017 (no releases)
    importpath = "google.golang.org/genproto",
)
