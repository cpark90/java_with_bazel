#WORKSPACE
workspace(name = "java_with_bazel")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

load("//:java_with_bazel_deps.bzl", "java_with_bazel_deps")
java_with_bazel_deps()


# rules_docker is not strictly necessary, but interesting if you want to create
# and/or push docker containers for the examples. The docker executable is
# needed only if you want to run an image using Bazel.

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load(
    "@io_bazel_rules_docker//java:image.bzl",
    _java_image_repos = "repositories",
)

_java_image_repos()


load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "org.springframework.boot:spring-boot-starter-web:2.1.5.RELEASE",
    ],
    repositories = [
        "https://jcenter.bintray.com",
    ]
)

maven_install(
    name = "server_app",
    artifacts = [
        "com.google.guava:guava:27.0-jre",
    ],
    repositories = [
        "https://repo1.maven.org/maven2",
    ],
)
