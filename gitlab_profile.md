# GitLab Profile Configuration (gitlab.com)

## 1. Profile Settings (Settings -> Profile)

- **Full Name**: `Matteo Valenti`
- **Job Title**: `Staff Systems Software Engineer & Storage Architect`
- **Bio** (205 chars / limit 250):
  ```text
  Systems engineer in Zurich. Obsessed with kernel-bypass I/O (io_uring), lock-free data topologies, and deterministic low-latency storage. Maintaining ring-kv & building crash-only distributed primitives.
  ```
- **Location**: `Zurich, Switzerland`
- **Website URL**: `https://github.com/johyojun13-coder`

---

## 2. GitLab Profile README.md (username/username repository)

```markdown
| [KR 한국어](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/ko.md) | [US English](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/README.md) | [JP 日本語](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/ja.md) | [CN 简体中文](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/zh-CN.md) | [ES Español](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/fr.md) | [DE Deutsch](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/de.md) | [RU Русский](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/ru.md) | [SA العربية](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/ar.md) | [IN हिन्दी](https://github.com/johyojun13-coder/johyojun13-coder/blob/main/docs/locales/hi.md) |

---

# Matteo Valenti

**Staff Systems Software Engineer & Storage Architect**  
Zurich, Switzerland · Bologna, Italy

> *"Hardware-aware data layout, asynchronous kernel-bypass pipelines, and deterministic failure reconciliation."*

I build storage primitives, asynchronous file engines, and continuous verification harnesses. On GitLab, my primary focus is maintaining continuous verification pipelines for low-level systems software: bare-metal performance regression test suites, custom QEMU/KVM virtualized kernel testbeds, and isolated micro-benchmarks targeting NVMe block storage.

---

## 🏗️ Active Infrastructure & GitLab Pipelines

| Workstream | Engine / Target | Focus | Pipeline Role |
| :--- | :--- | :--- | :--- |
| **`ring-kv-ci`** | Linux 6.x Zen / io_uring | Storage Engine | Regression test suites verifying zero memory allocation on hot read/write loops. |
| **`qemu-kernel-matrix`** | QEMU, KVM, BusyBox | Kernel Testbed | Multi-architecture matrix builds validating eBPF tracepoints across kernel revisions. |
| **`simd-bench-runner`** | GCC 14, Clang 18, Rust | Code Generation | Fine-grained cache-line eviction and branch misprediction telemetry generation. |
| **`raft-chaos-harness`** | Docker, tc-netem, Go | Network Faults | Deterministic network partition injection and split-brain recovery verification. |

---

## ⚙️ Core Technical Disciplines

```text
Languages:     Rust (nightly/stable), C++ (C++20/C++23), ISO C (C11), Go, Zig
Kernel & I/O:  Linux Kernel Internals, io_uring, O_DIRECT, POSIX AIO, epoll
Concurrency:   Lock-free rings, Hazard Pointers, Atomic operations, Memory barriers
CI/CD & Infra: GitLab CI/CD, QEMU/KVM, Docker, Bare-metal self-hosted runners, Perf
Tracing:       eBPF, bpftrace, ftrace, Valgrind/ASan/TSan, GDB
```

---

## 📐 System Invariants

1. **Deterministic Test Verification**: No integration test passes on flaky heuristics. Tests must either yield exit code 0 under extreme concurrency stress or fail explicitly with full memory dumps.
2. **Resource Isolation**: CI runners operate on dedicated pinning cores (`taskset`) and isolated CPU shielding (`cset`) to ensure latency measurements remain noise-free.
3. **Reproducible Builds**: All low-level binary artifacts are compiled against hermetic toolchains with bit-for-bit reproducibility.

---

## 📬 Connectivity & Mirrors

- **GitHub Profile**: [johyojun13-coder](https://github.com/johyojun13-coder)
- **Direct Mail**: `matteo.valenti.systems@gmail.com`
- **PGP Fingerprint**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
```
