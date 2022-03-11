# Bazel workspace created by @bazel/create 5.2.0

# Declares that this directory is the root of a Bazel workspace.
# See https://docs.bazel.build/versions/main/build-ref.html#workspace
workspace(
    # How this workspace would be referenced with absolute labels from another workspace
    name = "testworkpace",
)

load("//tools:bazel_deps.bzl", "fetch_dependencies")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

fetch_dependencies()

load("@build_bazel_rules_nodejs//:repositories.bzl", "build_bazel_rules_nodejs_dependencies")

build_bazel_rules_nodejs_dependencies()

# The npm_install rule runs yarn anytime the package.json or package-lock.json file changes.
# It also extracts any Bazel rules distributed in an npm package.
load("@build_bazel_rules_nodejs//:index.bzl", "npm_install")

npm_install(
    # Name this npm so that Bazel Label references look like @npm//package
    name = "npm",
    package_json = "//:package.json",
    package_lock_json = "//:package-lock.json",
)

load("@build_bazel_rules_nodejs//toolchains/esbuild:esbuild_repositories.bzl", "esbuild_repositories")

esbuild_repositories(npm_repository = "npm")


# VITE STUFF
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

VITE_COMMIT = "2790cd1964bf8a8c70c77ddc7ea32220ff000744"
VITE_SHA256 = "55f97743ec28e1b3ef24547d7f171a381cca46c8c296267bac32f77faec25075"

http_archive(
    name = "ubiquitous_tech_rules_vite",
    sha256 = VITE_SHA256,
    strip_prefix = "rules_vite-%s" % VITE_COMMIT,
    urls = ["https://github.com/ubiquitoustech/rules_vite/archive/%s.zip" % VITE_COMMIT],
)

load("@ubiquitous_tech_rules_vite//vite:repositories.bzl", "rules_vite_dependencies")

# This fetches the rules_vite dependencies, which are:
# - bazel_skylib
# - rules_nodejs
# If you want to have a different version of some dependency,
# you should fetch it *before* calling this.
# Alternatively, you can skip calling this function, so long as you've
# already fetched these dependencies.
rules_vite_dependencies()
