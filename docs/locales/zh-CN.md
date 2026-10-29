| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [BR Português](./pt-BR.md) | [SA العربية](./ar.md) |

---

# 马特奥·瓦伦蒂 (Matteo Valenti)

**系统软件工程师 / 存储引擎研发者**  
现居瑞士苏黎世 · 原籍意大利博洛尼亚  

> *"机械同理心（Mechanical Sympathy）、内核旁路 I/O，以及高核心并发下的确定性控制。"*

我专注于设计与实现超低延迟存储引擎、异步 I/O 架构和分布式日志底层组件。我的核心技术工作处于 Linux 内核底层、无锁并发数据结构与硬件感知内存布局的交界处。当生产系统由于 I/O 阻塞或互斥锁（Mutex）竞争而消耗无谓的 CPU 周期时，我便会深入探查其瓶颈根源。

---

## 🧭 当前研究重点与方向

- **NVMe 直接存取存储引擎**：基于 Linux `io_uring` 与分区块设备（ZBC/ZNS）构建高吞吐嵌入式键值数据库 `ring-kv`。
- **无锁预写日志（WAL）**：利用循环环形缓冲区（Ring Buffer）和零拷贝批量向量化处理，大幅降低分布式 Raft 状态机的 p99.9 尾延迟。
- **eBPF 系统级深度观测**：编写内核态追踪探针，精确定位高并发高吞吐服务器中的调度抖动及 NUMA 节点互联通信瓶颈。
- **严谨的微基准测试（Micro-benchmarking）**：针对底层内存分配器构建可复现的 L1/L2 缓存缺失及分支预测失败评测工具链。

---

## 🛠️ 开源代表项目

| 项目名称 | 技术栈 | 维护状态 | 项目描述 |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | 积极开发中 | 彻底消除用户态与内核态上下文切换开销的异步嵌入式 LSM-Tree 键值存储引擎。 |
| **`wal-compact`** | Rust, SIMD | 持续维护 | 具备向量化 CRC32 校验与并发快照压缩功能的零拷贝预写日志分段序列化组件。 |
| **`trace-sched`** | C, eBPF / BCC, Python | 持续维护 | 能够精准捕捉操作系统线程迁移成本与跨核 CPU 缓存失效损耗的 Linux 追踪探针套件。 |
| **`syn-drift`** | Go, POSIX Timers | 积极开发中 | 用于纳秒/微秒级 PTP/NTP 硬件时钟偏差分析的高精度时钟基准与同步监控守护进程。 |

---

## 💻 技术栈与工程工具链

### 核心系统语言
```text
主要语言:   Rust (nightly 与 stable), 现代 C++ (C++20 / C++23), ISO C (C11/C17)
辅助语言:   Go, Zig, Bash, Python (用于系统遥测数据分析与脚本开发)
汇编指令:   x86_64 SIMD (AVX-512 / AVX2), 基础 ARM64 NEON 内联函数
```

### 内核、I/O 与高性能网络子系统
| 领域 | 核心技术与架构框架 |
| :--- | :--- |
| **异步 I/O** | `io_uring`, epoll, kqueue, 直接 I/O (`O_DIRECT`), 异步文件描述符 |
| **内核可观测性** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, 内核 Tracepoints |
| **并发控制原语** | 原子指令, 内存屏障（Memory Barriers）, 无锁环形队列, Hazard Pointers, RCU |
| **数据结构拓扑** | LSM-Tree, Bw-Tree, 跳表 (Skip List), 基数树 (Radix Tree), 环形缓冲区 |
| **调试与性能剖析** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 架构工程哲学

1. **硬件感知设计（Mechanical Sympathy）**  
   物理内存布局决定了程序的极限性能。所有核心数据结构均对齐至 64 字节缓存行（Cache Line）边界以杜绝伪共享（False Sharing）；摒弃链式指针寻址，坚持顺序内存访问以最大化硬件预取器效能。

2. **零拷贝（Zero-Copy）作为硬性底线**  
   在关键数据流热点路径上的堆内存动态分配被视为架构设计缺陷。在操作系统底层能力允许的范围内，所有从磁盘或网卡读入内存的数据均通过固定内存（Pinned Memory）和零拷贝缓冲区流转。

3. **确定性故障隔离域**  
   分布式系统的故障模式不可预见且具有级联性。我坚持 Crash-Only 软件哲学：依靠清晰的状态对齐、具备自愈能力的预写日志恢复机制以及可复现的混沌工程（Chaos Testing），而非依赖脆弱复杂的容错启发式逻辑。

---

## 🖥️ 个人工作站配置

```text
操作系统:   Debian GNU/Linux (Sid / Testing) 与 Arch Linux (定制 zen 内核)
编辑器:     Neovim (基于 Lua 的极简配置, 驱动 rust-analyzer 与 clangd)
终端环境:   Alacritty + tmux
Shell:      zsh (简洁提示符, 启用 vi-mode 键盘模式)
显示输出:   双 27 英寸 4K 显示器 (竖屏/横屏组合布局)
核心硬件:   AMD Ryzen 9 7950X (16核32线程), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ 代码之外的生活

- **浓缩咖啡萃取物理学**: 针对平刀盘（Flat Burr）磨豆机进行微米级校准，并在改装的双锅炉手动杠杆拉杆机上跟踪压力与流量分布曲线。
- **模块化模拟音频合成**: 组装 Eurorack 模拟合成器模块，探索时钟分频器与步进音序器的硬件级物理跳线实验。
- **抱石与高山攀登**: 只要天气与日程允许，便前往瑞士阿尔卑斯山脉的花岗岩岩壁攀岩，在石缝中寻找力量与内心的平衡。

---

## 📬 联系方式与公开密钥

- **常驻地点**: 瑞士苏黎世 (8005)
- **电子邮箱**: `matteo.valenti.systems@gmail.com`
- **PGP 指纹**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix 协议**: `@mvalenti:matrix.org`
