# Copyright 2023 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# RiscV sim library for use with codelabs

package(
    default_applicable_licenses = ["//:license"],
    default_visibility = ["//visibility:public"],
)

cc_library(
    name = "riscv_simple_state",
    srcs = [
        "riscv_simple_state.cc",
    ],
    hdrs = [
        "riscv_register.h",
        "riscv_simple_state.h",
    ],
    deps = [
        "@com_google_absl//absl/container:flat_hash_map",
        "@com_google_absl//absl/functional:any_invocable",
        "@com_google_absl//absl/log",
        "@com_google_absl//absl/log:check",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/status:statusor",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/types:any",
        "@com_google_mpact-sim//mpact/sim/generic:arch_state",
        "@com_google_mpact-sim//mpact/sim/generic:core",
        "@com_google_mpact-sim//mpact/sim/generic:instruction",
        "@com_google_mpact-sim//mpact/sim/generic:type_helpers",
        "@com_google_mpact-sim//mpact/sim/util/memory",
    ],
)

cc_library(
    name = "rv32i_top",
    srcs = [
        "rv32i_top.cc",
    ],
    hdrs = [
        "rv32i_top.h",
    ],
    deps = [
        ":riscv_simple_state",
        "//riscv_full_decoder/solution:riscv32i_decoder",
        "//riscv_isa_decoder/solution:riscv32i_isa",
        "@com_google_absl//absl/functional:bind_front",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/status:statusor",
        "@com_google_absl//absl/strings",
        "@com_google_mpact-riscv//riscv:riscv32_htif_semihost",
        "@com_google_mpact-riscv//riscv:riscv_breakpoint",
        "@com_google_mpact-riscv//riscv:riscv_state",
        "@com_google_mpact-sim//mpact/sim/generic:component",
        "@com_google_mpact-sim//mpact/sim/generic:core",
        "@com_google_mpact-sim//mpact/sim/generic:core_debug_interface",
        "@com_google_mpact-sim//mpact/sim/generic:decode_cache",
        "@com_google_mpact-sim//mpact/sim/util/memory",
    ],
)

cc_binary(
    name = "rv32i_sim",
    srcs = [
        "rv32i_sim.cc",
    ],
    copts = ["-O3"],
    data = [
        "hello_rv32i.elf",
    ],
    deps = [
        ":rv32i_top",
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/flags:parse",
        "@com_google_absl//absl/status",
        "@com_google_absl//absl/strings",
        "@com_google_mpact-riscv//riscv:debug_command_shell",
        "@com_google_mpact-riscv//riscv:riscv32_htif_semihost",
        "@com_google_mpact-sim//mpact/sim/generic:core",
        "@com_google_mpact-sim//mpact/sim/proto:component_data_cc_proto",
        "@com_google_mpact-sim//mpact/sim/util/memory",
        "@com_google_mpact-sim//mpact/sim/util/program_loader:elf_loader",
    ],
)
