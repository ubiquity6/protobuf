workspace(name = "com_google_protobuf")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

new_local_repository(
    name = "submodule_gmock",
    build_file = "@//:third_party/googletest/BUILD.bazel",
    path = "third_party/googletest",
)

http_archive(
    name = "six",
    url = "https://pypi.python.org/packages/source/s/six/six-1.9.0.tar.gz",
    sha256 = "e24052411fc4fbd1f672635537c3fc2330d9481b18c0317695b46259512c91d5",
    strip_prefix = "six-1.9.0/",
    type = "tar.gz",
    build_file_content = """
# Rename six.py to __init__.py
genrule(
    name = "rename",
    srcs = ["six.py"],
    outs = ["__init__.py"],
    cmd = "cat $< >$@",
)
py_library(
   name = "six",
   srcs = [":__init__.py"],
   visibility = ["//visibility:public"],
)""",
    )

http_archive(
    name = "bazel_skylib",
    sha256 = "bbccf674aa441c266df9894182d80de104cabd19be98be002f6d478aaa31574d",
    strip_prefix = "bazel-skylib-2169ae1c374aab4a09aa90e65efe1a3aad4e279b",
    urls = ["https://github.com/bazelbuild/bazel-skylib/archive/2169ae1c374aab4a09aa90e65efe1a3aad4e279b.tar.gz"],
)

http_archive(
    name = "net_zlib",
    build_file = "//:third_party/zlib.BUILD",
    sha256 = "c3e5e9fdd5004dcb542feda5ee4f0ff0744628baf8ed2dd5d66f8ca1197cb1a1",
    strip_prefix = "zlib-1.2.11",
    urls = ["https://zlib.net/zlib-1.2.11.tar.gz"],
)

bind(
    name = "python_headers",
    actual = "//util/python:python_headers",
)

bind(
    name = "gtest",
    actual = "@submodule_gmock//:gtest",
)

bind(
    name = "gtest_main",
    actual = "@submodule_gmock//:gtest_main",
)

maven_jar(
    name = "guava_maven",
    artifact = "com.google.guava:guava:18.0",
)

bind(
    name = "guava",
    actual = "@guava_maven//jar",
)

maven_jar(
    name = "gson_maven",
    artifact = "com.google.code.gson:gson:2.7",
)

bind(
    name = "gson",
    actual = "@gson_maven//jar",
)

bind(
    name = "zlib",
    actual = "@net_zlib//:zlib",
)
