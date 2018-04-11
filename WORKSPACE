workspace(name = "angular_flex_layout")

# Add nodejs rules
http_archive(
    name = "build_bazel_rules_nodejs",
    url = "https://github.com/bazelbuild/rules_nodejs/archive/0.7.0.zip",
    strip_prefix = "rules_nodejs-0.7.0",
    sha256 = "d0cecf6b149d431ee8349f683d1db6a2a881ee81d8066a66c1b112a4b02748de",
)

# NOTE: this rule installs nodejs, npm, and yarn, but does NOT install
# your npm dependencies. You must still run the package manager.
load("@build_bazel_rules_nodejs//:defs.bzl", "check_bazel_version", "node_repositories")

check_bazel_version("0.11.1")
node_repositories(package_json = ["//:package.json"])

# Add sass rules
git_repository(
  name = "io_bazel_rules_sass",
  remote = "https://github.com/bazelbuild/rules_sass.git",
  tag = "0.0.3",
)

load("@io_bazel_rules_sass//sass:sass.bzl", "sass_repositories")
sass_repositories()

# Add TypeScript rules
http_archive(
  name = "build_bazel_rules_typescript",
  url = "https://github.com/bazelbuild/rules_typescript/archive/0.12.0.zip",
  strip_prefix = "rules_typescript-0.12.0",
  sha256 = "60c17e558fdcb66783f39418c8dfd4858c8fd748089e42ddf91e75a853471244",
)

# Setup TypeScript Bazel workspace
load("@build_bazel_rules_typescript//:defs.bzl", "ts_setup_workspace")
ts_setup_workspace()

# Add Angular rules
local_repository(
  name = "angular",
  path = "node_modules/@angular/bazel",
)

# Add rxjs
local_repository(
  name = "rxjs",
  path = "node_modules/rxjs/src",
)

# Point to the apps workspace just so that Bazel doesn't descend into it
# when expanding the //... pattern
local_repository(
    name = "demo_app",
    path = "src/apps/demo-app",
)

# Point to the apps workspace just so that Bazel doesn't descend into it
# when expanding the //... pattern
local_repository(
    name = "hello_world_app",
    path = "src/apps/hello-world",
)

# Point to the apps workspace just so that Bazel doesn't descend into it
# when expanding the //... pattern
local_repository(
    name = "universal_app",
    path = "src/apps/universal-app",
)

# This commit matches the version of buildifier in angular/ngcontainer
# If you change this, also check if it matches the version in the angular/ngcontainer
# version in /.circleci/config.yml
BAZEL_BUILDTOOLS_VERSION = "70bc7843bb9950fece2bc014ed16de03419e36e2"

# The Bazel buildtools repo contains tools like the BUILD file formatter, buildifier
http_archive(
    name = "com_github_bazelbuild_buildtools",
    # Note, this commit matches the version of buildifier in angular/ngcontainer
    url = "https://github.com/bazelbuild/buildtools/archive/%s.zip" % BAZEL_BUILDTOOLS_VERSION,
    strip_prefix = "buildtools-%s" % BAZEL_BUILDTOOLS_VERSION,
    sha256 = "367c23a5fe7fc2a7cb57863d3718b4149f0e57426c48c8ad54c45348a0b53cc1",
)

# Fetching the Bazel source code allows us to compile the Skylark linter
http_archive(
    name = "io_bazel",
    url = "https://github.com/bazelbuild/bazel/archive/5a35e72f9e97c06540c479f8c31512fb4656202f.zip",
    strip_prefix = "bazel-5a35e72f9e97c06540c479f8c31512fb4656202f",
    sha256 = "ed33a52874c14e3b487fb50f390c541fab9c81a33d986d38fb01766a66dbcd21",
)

# Parts of the build toolchain are written in Go, such as ts_devserver and buildifier
# Bazel doesn't support transitive WORKSPACE deps, so we must repeat them here.
http_archive(
    name = "io_bazel_rules_go",
    url = "https://github.com/bazelbuild/rules_go/releases/download/0.10.3/rules_go-0.10.3.tar.gz",
    sha256 = "feba3278c13cde8d67e341a837f69a029f698d7a27ddbb2a202be7a10b22142a",
)

load("@io_bazel_rules_go//go:def.bzl", "go_rules_dependencies", "go_register_toolchains")

go_rules_dependencies()

go_register_toolchains()
