# bazel-kotlinx-repro

Repro for Bazel where syncing fails in IntelliJ because the kotlinx.collections reference cannot be resolved even though
the dependency is included in the BUILD file.

Even trying to build the project in the terminal causes weird errors that I don't even know where to start debugging.

```bash
$ bazel build //kotlinx/repro:app
INFO: Analyzed target //kotlinx/repro:app (65 packages loaded, 1539 targets configured).
INFO: From Building external/bazel_tools/src/tools/android/java/com/google/devtools/build/android/dexer/DexFileSplitter.jar (5 source files) and running annotation processors (AutoValueProcessor) [for tool]:
warning: [options] source value 8 is obsolete and will be removed in a future release
warning: [options] target value 8 is obsolete and will be removed in a future release
warning: [options] To suppress warnings about obsolete options, use -Xlint:-options.
INFO: From Building external/rules_jvm_external/private/tools/java/rules/jvm/external/libbyte-streams.jar (1 source file) [for tool]:
warning: [options] source value 8 is obsolete and will be removed in a future release
warning: [options] target value 8 is obsolete and will be removed in a future release
warning: [options] To suppress warnings about obsolete options, use -Xlint:-options.
INFO: From Building external/rules_jvm_external/private/tools/java/rules/jvm/external/zip/libzip.jar (1 source file) [for tool]:
warning: [options] source value 8 is obsolete and will be removed in a future release
warning: [options] target value 8 is obsolete and will be removed in a future release
warning: [options] To suppress warnings about obsolete options, use -Xlint:-options.
INFO: From Building external/rules_jvm_external/private/tools/java/rules/jvm/external/jar/AddJarManifestEntry.jar (1 source file) [for tool]:
warning: [options] source value 8 is obsolete and will be removed in a future release
warning: [options] target value 8 is obsolete and will be removed in a future release
warning: [options] To suppress warnings about obsolete options, use -Xlint:-options.
INFO: From Building external/bazel_tools/src/tools/android/java/com/google/devtools/build/android/r8/libr8.jar (16 source files) and running annotation processors (AutoValueProcessor) [for tool]:
warning: [options] source value 8 is obsolete and will be removed in a future release
warning: [options] target value 8 is obsolete and will be removed in a future release
warning: [options] To suppress warnings about obsolete options, use -Xlint:-options.
ERROR: /private/var/tmp/_bazel_rururu/285fa57efc2ee9900a31455eb42fc32c/external/maven/BUILD:113:11: Desugaring external/maven/v1/https/maven.google.com/androidx/annotation/annotation/1.8.1/processed_annotation-1.8.1.jar for Android failed: Worker process did not return a WorkResponse:

---8<---8<--- Start of log, file at /private/var/tmp/_bazel_rururu/285fa57efc2ee9900a31455eb42fc32c/bazel-workers/worker-91-Desugar.log ---8<---8<---
(empty)
---8<---8<--- End of log ---8<---8<---
Target //kotlinx/repro:app failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 22.648s, Critical Path: 4.54s
INFO: 388 processes: 25 internal, 352 darwin-sandbox, 11 worker.
ERROR: Build did NOT complete successfully
```

The desugaring failure is never consistent either on which dependency it fails on

```
ERROR: /private/var/tmp/_bazel_rururu/285fa57efc2ee9900a31455eb42fc32c/external/rules_kotlin/kotlin/compiler/BUILD.bazel:22:22: Desugaring lib/kotlin-stdlib.jar for Android failed: Worker process did not return a WorkResponse:

---8<---8<--- Start of log, file at /private/var/tmp/_bazel_rururu/285fa57efc2ee9900a31455eb42fc32c/bazel-workers/worker-94-Desugar.log ---8<---8<---
(empty)
---8<---8<--- End of log ---8<---8<---
```

```
ERROR: /private/var/tmp/_bazel_rururu/285fa57efc2ee9900a31455eb42fc32c/external/maven/BUILD:1327:11: Desugaring external/maven/v1/https/maven.google.com/androidx/lifecycle/lifecycle-common-java8/2.6.2/processed_lifecycle-common-java8-2.6.2.jar for Android failed: Worker process did not return a WorkResponse:

---8<---8<--- Start of log, file at /private/var/tmp/_bazel_rururu/285fa57efc2ee9900a31455eb42fc32c/bazel-workers/worker-93-Desugar.log ---8<---8<---
(empty)
---8<---8<--- End of log ---8<---8<---
```