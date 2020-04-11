load("@io_bazel_rules_go//go:def.bzl", "go_binary", "go_library")
package(default_visibility = ["//visibility:public"])
load("@bazel_gazelle//:def.bzl", "gazelle")

# gazelle:prefix github.com/kibab/fractalizer
gazelle(name = "gazelle")

go_library(
    name = "go_default_library",
    srcs = ["fractalizer.go"],
    importpath = "github.com/kibab/fractalizer",
)

go_binary(
    name = "fractalizer",
    embed = [":go_default_library"],
)
