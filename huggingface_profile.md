# Hugging Face Profile Configuration (huggingface.co)

## 1. Account Settings (Settings -> Profile)

- **Full Name**: `Matteo Valenti`
- **Bio** (Markdown supported):
  ```text
  Systems software engineer exploring the physical boundaries of machine learning runtimes: zero-copy model weight deserialization via `io_uring`, NVMe direct tiering for KV-cache state, and custom AVX-512 / SIMD quantization kernels.
  ```
- **GitHub Username**: `johyojun13-coder`
- **Homepage / Website**: `https://github.com/johyojun13-coder`
- **Interests (Tags)**:
  - `low-latency-inference`
  - `kv-cache-offloading`
  - `io-uring`
  - `custom-kernels`
  - `simd-quantization`

---

## 2. Hugging Face Profile Introduction Body (Overview & Portfolio)

```markdown
# Matteo Valenti

**Systems & Storage Engineer · ML Runtime & Low-Latency Systems**  
Zurich, Switzerland · Bologna, Italy

> *"Treating LLM inference as a hardware-level streaming and memory bandwidth orchestration problem."*

I approach machine learning from the perspective of low-level systems programming: memory layout, PCIe saturation, zero-copy deserialization, and cache-conscious tensor operations. Rather than model architecture design, my work centers on what happens between the NVMe controller, the host RAM, and the accelerator memory bus.

---

## 🔬 Systems Focus in ML Infrastructure

- **Zero-Copy Tensor Streaming**: Bypassing OS page caches with direct NVMe transfers (`O_DIRECT` + `io_uring`) to feed weights directly into pinned buffers at full hardware line rates.
- **Hierarchical KV-Cache Tiering**: Implementing high-throughput out-of-VRAM key-value cache swapping algorithms on Zoned Namespaces (ZNS) solid-state storage.
- **Hardware-Aware Quantization Kernels**: Hand-tuned micro-kernels leveraging x86_64 AVX-512 and ARM64 NEON instructions for ultra-fast 2-bit / 4-bit matrix-vector multiplications on CPU and edge hardware.
- **Deterministic Latency Profiling**: In-kernel eBPF instrumentation tracking context switches, memory allocation pauses, and PCIe bus congestion during token generation phases.

---

## 📦 Projects, Repositories & Artifacts

| Artifact | Type | Stack | Description |
| :--- | :--- | :--- | :--- |
| **`ring-kv-cache`** | Tool / Runtime | Rust, C, Linux `io_uring` | Embedded storage engine designed specifically for offloading long-context (128k+) KV-caches to NVMe with sub-millisecond page faults. |
| **`safetensors-fastload`** | Library | C++, Rust, SIMD | Experimental zero-copy `.safetensors` weight loader that saturates PCIe Gen4/Gen5 bus limits without intermediate userspace memory allocations. |
| **`avx512-quant-bench`** | Dataset / Benchmark | Python, C, Shell | Rigorous cache-miss and IPC (instructions per cycle) performance dataset comparing 4-bit quantization kernels across modern CPU microarchitectures. |

---

## 🛠️ Systems Toolchain

```text
Low-Level:     Rust, Modern C++ (C++20), ISO C, x86_64 SIMD (AVX-512/AVX2), basic CUDA
Kernel/IO:     Linux io_uring, eBPF, O_DIRECT, hugepages, POSIX shared memory
Profiling:     perf, Valgrind, bpftrace, NVIDIA Nsight Systems, VTune
```

---

## 📬 Contact & Links

- **GitHub**: [github.com/johyojun13-coder](https://github.com/johyojun13-coder)
- **Direct Mail**: `matteo.valenti.systems@gmail.com`
- **PGP Fingerprint**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
```
