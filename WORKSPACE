load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "db2b2d35293f405430f553bc7a865a8749a8ef60c30287e90d2b278c32771afe",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.22.3/rules_go-v0.22.3.tar.gz",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.22.3/rules_go-v0.22.3.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_rules_dependencies", "go_register_toolchains")

go_rules_dependencies()

go_register_toolchains()
http_archive(
    name = "bazel_gazelle",
    urls = [
        "https://storage.googleapis.com/bazel-mirror/github.com/bazelbuild/bazel-gazelle/releases/download/v0.20.0/bazel-gazelle-v0.20.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.20.0/bazel-gazelle-v0.20.0.tar.gz",
    ],
    sha256 = "d8c45ee70ec39a57e7a05e5027c32b1576cc7f16d9dd37135b0eddde45cf1b10",
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

# Download the rules_docker repository at release v0.14.1
http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "dc97fccceacd4c6be14e800b2a00693d5e8d07f69ee187babfd04a80a9f8e250",
    strip_prefix = "rules_docker-0.14.1",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.14.1/rules_docker-v0.14.1.tar.gz"],
)

load("@io_bazel_rules_docker//toolchains/docker:toolchain.bzl",
    docker_toolchain_configure="toolchain_configure"
)

docker_toolchain_configure(
  name = "docker_config",
  # OPTIONAL: Path to a directory which has a custom docker client config.json.
  # See https://docs.docker.com/engine/reference/commandline/cli/#configuration-files
  # for more details.
  #client_config="<enter absolute path to your docker config directory here>",
  # OPTIONAL: Path to the docker binary.
  # Should be set explcitly for remote execution.
  docker_path="/usr/local/bin/docker",
  # OPTIONAL: Path to the gzip binary.
  # Either gzip_path or gzip_target should be set explcitly for remote execution.
  #gzip_path="<enter absolute path to the gzip binary (in the remote exec env) here>",
  # OPTIONAL: Bazel target for the gzip tool.
  # Either gzip_path or gzip_target should be set explcitly for remote execution.
  #gzip_target="<enter absolute path (i.e., must start with repo name @...//:...) to an executable gzip target>",
  # OPTIONAL: Path to the xz binary.
  # Should be set explcitly for remote execution.
  #xz_path="<enter absolute path to the xz binary (in the remote exec env) here>",
  # OPTIONAL: List of additional flags to pass to the docker command.
  #docker_flags = [
  #  "--tls",
  #  "--log-level=info",
  #],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")
container_deps()


load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_image", "container_pull"
)

container_pull(
  name = "deb10",
  registry = "gcr.io",
  repository = "distroless/base-debian10",
  # 'tag' is also supported, but digest is encouraged for reproducibility.
  digest = "sha256:ad9cb88a4d4e6969b44137de488c2a21e0e53d32a7eed601b39bf760bfdf14d0",
)
