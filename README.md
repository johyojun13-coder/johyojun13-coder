| [KR 한국어](./docs/locales/ko.md) | [US English](./README.md) | [JP 日本語](./docs/locales/ja.md) | [CN 简体中文](./docs/locales/zh-CN.md) | [ES Español](./docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./docs/locales/fr.md) | [DE Deutsch](./docs/locales/de.md) | [RU Русский](./docs/locales/ru.md) | [SA العربية](./docs/locales/ar.md) | [IN हिन्दी](./docs/locales/hi.md) |

---: | :---: | :---: | :---: | :---: |
| [FR Français](./docs/locales/fr.md) | [DE Deutsch](./docs/locales/de.md) | [RU Русский](./docs/locales/ru.md) | [BR Português](./docs/locales/pt-BR.md) | [SA العربية](./docs/locales/ar.md) |

---

# Matteo Valenti

**Systems Software Engineer & Storage Engine Craftsman**  
Based in Zurich, Switzerland · Originally from Bologna, Italy  

> *"Mechanical sympathy, kernel-bypass I/O, and deterministic concurrency under high core counts."*

I design and build low-latency storage engines, asynchronous I/O architectures, and distributed log primitives. Most of my work sits at the intersection of Linux kernel internals, lock-free concurrency, and hardware-aware data structures. When an application stalls on I/O wait or burns cycles in mutex contention, that is where I dig in.

---

## 🧭 Focus & Active Investigations

- **NVMe Direct-Access Engines**: Designing `ring-kv`, an experimental embedded key-value store built around `io_uring` and zoned block devices (ZBC/ZNS).
- **Lockless Write-Ahead Logging**: Reducing p99.9 write tail latency in distributed Raft state machines via circular ring buffers and vectorized zero-copy batching.
- **eBPF-driven Systems Telemetry**: Writing in-kernel tracing probes to identify scheduling jitter and NUMA-node interconnect saturation on high-throughput server workloads.
- **Micro-benchmarking Rigor**: Building reproducible cache-miss and branch-misprediction testing suites for low-level memory allocators.

---

## 🛠️ Featured Open-Source Projects

| Repository | Stack | Status | Description |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | Active | Asynchronous, embedded LSM-tree key-value store eliminating userspace-to-kernel context switch overheads. |
| **`wal-compact`** | Rust, SIMD | Maintained | Zero-copy Write-Ahead Log segment serializer with vectorized CRC32 checksumming and concurrent snapshot compaction. |
| **`trace-sched`** | C, eBPF / BCC, Python | Maintained | Lightweight Linux tracing probe suite pinpointing OS thread migration overhead and cross-core cache invalidations. |
| **`syn-drift`** | Go, POSIX Timers | Active | Microsecond-granularity PTP/NTP hardware clock skew analyzer and timespec monitoring daemon. |

---

## 💻 Technical Capabilities & Tooling

### Core Systems & Languages
```text
Primary:       Rust (nightly & stable), Modern C++ (C++20 / C++23), ISO C (C11/C17)
Supplementary: Go, Zig, Bash, Python (for telemetry analysis & bindings)
Assembly:      x86_64 SIMD (AVX-512 / AVX2), basic ARM64 NEON intrinsics
```

### Kernel, I/O & Networking Subsystems
| Domain | Technologies & Frameworks |
| :--- | :--- |
| **Asynchronous I/O** | `io_uring`, epoll, kqueue, direct I/O (`O_DIRECT`), asynchronous file descriptors |
| **Kernel Observation** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, kernel tracepoints |
| **Concurrency Primitives** | Atomic instructions, memory barriers, lock-free ring buffers, Hazard Pointers, RCU |
| **Data Topologies** | Log-Structured Merge-Trees (LSM), Bw-Trees, Skip Lists, Radix Trees, Ring Buffers |
| **Debugging & Profiling** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 Engineering Principles

1. **Hardware-Aware Design (Mechanical Sympathy)**  
   Data layout dictates performance. Structs are aligned to 64-byte cache line boundaries to prevent false sharing. Sequential access patterns are favored over pointer chasing to maximize L1/L2 prefetcher utilization.

2. **Zero-Copy as a Hard Rule**  
   Memory allocations inside the hot data path are treated as architecture defects. Every byte transferred from disk or network to memory is pinned, sliced, and moved through zero-copy buffers whenever OS primitives permit.

3. **Deterministic Failure Domains**  
   Distributed systems fail in non-obvious ways. I prioritize crash-only software designs: clear state reconciliation, self-healing WAL recovery, and reproducible chaos test suites over complex, brittle recovery heuristics.

---

## 🖥️ Daily Driver Environment

```text
OS:         Debian GNU/Linux (Sid / Testing) & Arch Linux (custom zen kernel)
Editor:     Neovim (Lua-driven, LSP via rust-analyzer & clangd)
Terminal:   Alacritty + tmux
Shell:      zsh with minimal prompt (vi-mode enabled)
Monitors:   Dual 27" 4K in portrait/landscape configuration
Hardware:   AMD Ryzen 9 7950X (16c/32t), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ Beyond Code

- **Espresso Extraction Dynamics**: Dialing in flat burr grinders and tracking pressure/flow profiling graphs on a modified dual-boiler manual lever machine.
- **Modular Audio Synthesis**: Patching Eurorack analogue synthesizer modules, clock dividers, and step sequencers.
- **Bouldering & Alpine Scrambling**: Finding grip on granite faces across the Swiss Alps whenever weather and schedule align.

---

## 📬 Contact & Public Keys

- **Location**: Zurich (8005), Switzerland
- **Direct Mail**: `matteo.valenti.systems@gmail.com`
- **PGP Fingerprint**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix**: `@mvalenti:matrix.org`
