load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Kotlin
RULES_KOTLIN_VERSION = "2.0.0"

RULES_KOTLIN_SHA = "d89723cc9ebbb7bdb2ebaca1af7d2383e074615643cf97a366b758a76b7dc443"

http_archive(
    name = "rules_kotlin",
    sha256 = RULES_KOTLIN_SHA,
    urls = ["https://github.com/bazelbuild/rules_kotlin/releases/download/v{v}/rules_kotlin-v{v}.tar.gz".format(v = RULES_KOTLIN_VERSION)],
)

load(
    "@rules_kotlin//kotlin:repositories.bzl",
    "kotlin_repositories",
)

kotlin_repositories()

register_toolchains("//:kotlin_toolchain")

# Android
RULES_ANDROID_VERSION = "0.1.1"

RULES_ANDROID_SHA = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806"

http_archive(
    name = "rules_android",
    sha256 = RULES_ANDROID_SHA,
    strip_prefix = "rules_android-%s" % RULES_ANDROID_VERSION,
    urls = ["https://github.com/bazelbuild/rules_android/archive/v%s.zip" % RULES_ANDROID_VERSION],
)

load("@rules_android//android:rules.bzl", "android_sdk_repository")

android_sdk_repository(
    name = "androidsdk",
    api_level = 34,
    build_tools_version = "34.0.0",
)

# JVM External
RULES_JVM_EXTERNAL_VERSION = "4.5"

RULES_JVM_EXTERNAL_SHA = "b17d7388feb9bfa7f2fa09031b32707df529f26c91ab9e5d909eb1676badd9a6"

http_archive(
    name = "rules_jvm_external",
    sha256 = RULES_JVM_EXTERNAL_SHA,
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_VERSION,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_VERSION,
)

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

load("//third_party:maven_dependencies.bzl", "MAVEN_ARTIFACTS")
load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = MAVEN_ARTIFACTS,
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
    version_conflict_policy = "pinned",
)
