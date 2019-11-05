# rules_python_external

Contains Bazel rules to fetch and install Python dependencies from a requirements.txt file.

## Usage

In `requirements.txt`
```
cryptography[test, docs]==2.8
boto3==1.9.253
```

In `WORKSPACE`
```
rules_python_external_version = "37dad8910495ad71bae391db7a843a0f7a3ea902"

git_repository(
    name = "rules_python_external",
    commit = rules_python_external_version,
    remote = "git@github.com:dillon-giacoppo/rules_python_external.git",
    shallow_since = "1572846707 +1100",
)


load("@rules_python_external//:defs.bzl", "pip_repository")

pip_repository(
    name = "py_deps",
    requirements = "//:requirements.txt",
)
```

In `BUILD`
```
load("@py_deps//:requirements.bzl", "requirement")

py_binary(
    name = "main",
    srcs = ["main.py"],
    deps = [
        requirement("boto3"),
    ],
)
```
