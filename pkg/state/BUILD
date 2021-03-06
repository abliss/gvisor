load("//tools:defs.bzl", "go_library", "go_test", "proto_library")
load("//tools/go_generics:defs.bzl", "go_template_instance")

package(licenses = ["notice"])

go_template_instance(
    name = "addr_range",
    out = "addr_range.go",
    package = "state",
    prefix = "addr",
    template = "//pkg/segment:generic_range",
    types = {
        "T": "uintptr",
    },
)

go_template_instance(
    name = "addr_set",
    out = "addr_set.go",
    consts = {
        "minDegree": "10",
    },
    imports = {
        "reflect": "reflect",
    },
    package = "state",
    prefix = "addr",
    template = "//pkg/segment:generic_set",
    types = {
        "Key": "uintptr",
        "Range": "addrRange",
        "Value": "reflect.Value",
        "Functions": "addrSetFunctions",
    },
)

go_library(
    name = "state",
    srcs = [
        "addr_range.go",
        "addr_set.go",
        "decode.go",
        "encode.go",
        "encode_unsafe.go",
        "map.go",
        "printer.go",
        "state.go",
        "stats.go",
    ],
    marshal = False,
    stateify = False,
    visibility = ["//:sandbox"],
    deps = [
        ":object_go_proto",
        "@com_github_golang_protobuf//proto:go_default_library",
    ],
)

proto_library(
    name = "object",
    srcs = ["object.proto"],
    visibility = ["//:sandbox"],
)

go_test(
    name = "state_test",
    timeout = "long",
    srcs = ["state_test.go"],
    library = ":state",
)
