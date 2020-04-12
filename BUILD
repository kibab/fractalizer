load("@io_bazel_rules_go//go:def.bzl", "go_binary", "go_library")
load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_image", "container_pull", "container_push"
)
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
    goos = "linux",
    embed = [":go_default_library"],
)

container_image(
    name = "fractalizer_container",
    base = "@deb10//image",
    files = ["//:fractalizer"],
    entrypoint = [
        "/fractalizer"
        ],
)

container_push(
  name = "fractalizer_container_push",
  image = ":fractalizer_container",
  format = "Docker",
  registry = "gcr.io",
  repository = "kibab-fbsd-01/fractalizer",
  tag = "dev2",
)