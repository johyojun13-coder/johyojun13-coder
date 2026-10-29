| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [BR Português](./pt-BR.md) | [SA العربية](./ar.md) |

---

# 마테오 발렌티 (Matteo Valenti)

**시스템 소프트웨어 엔지니어 & 스토리지 엔진 빌더**  
스위스 취리히 거주 · 이탈리아 볼로냐 출신  

> *"기계적 공감(Mechanical Sympathy), 커널 바이패스 I/O, 고다핵 환경에서의 결정론적 동시성 제어."*

초저지연 스토리지 엔진, 비동기 I/O 파이프라인, 분산 로그 프리미티브를 설계하고 개발합니다. 저의 주된 작업 영역은 리눅스 커널 내부 구조, 락프리 동시성 자료구조, 하드웨어 친화적 메모리 아키텍처의 교차점에 위치합니다. 애플리케이션이 I/O 대기로 멈추거나 뮤텍스 경합으로 CPU 사이클을 낭비할 때, 그 병목의 근본 원인을 파고듭니다.

---

## 🧭 현재 집중 중인 연구 및 작업

- **NVMe 직접 제어 엔진**: 리눅스 `io_uring`과 존 블록 디바이스(ZBC/ZNS)를 결합한 초고속 임베디드 Key-Value 스토리지 `ring-kv` 설계.
- **락프리 Write-Ahead Logging**: 링 버퍼 순환 구조와 제로카피 배치 처리를 적용하여 분산 Raft 상태 머신의 p99.9 쓰기 꼬리 지연시간 단축.
- **eBPF 기반 시스템 텔레메트리**: 고처리량 서버 환경에서 스케줄러 지터와 NUMA 노드 간 인터커넥트 병목을 감지하는 커널 내장 트레이싱 프로브 개발.
- **마이크로 벤치마크 검증**: 저수준 메모리 할당자를 위한 L1/L2/L3 캐시 미스 및 분기 예측 실패 재현 테스트 스위트 구축.

---

## 🛠️ 주요 오픈소스 프로젝트

| 프로젝트 | 기술 스택 | 상태 | 설명 |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | 개발 중 | 유저 영역과 커널 간의 컨텍스트 스위칭 오버헤드를 원천 차단한 비동기 임베디드 LSM-Tree 스토리지 엔진. |
| **`wal-compact`** | Rust, SIMD | 유지보수 중 | 벡터화된 CRC32 무결성 검증과 동시성 스냅샷 컴팩션을 지원하는 제로카피 Write-Ahead Log 세그먼트 직렬화 라이브러리. |
| **`trace-sched`** | C, eBPF / BCC, Python | 유지보수 중 | 운영체제 스레드 마이그레이션 오버헤드와 코어 간 캐시 무효화 현상을 핀포인트 추적하는 리눅스 트레이싱 도구. |
| **`syn-drift`** | Go, POSIX Timers | 개발 중 | 마이크로초 단위의 PTP/NTP 하드웨어 클록 드리프트를 실시간 측정 및 분석하는 정밀 타임스탬프 데몬. |

---

## 💻 기술 스택 및 도구

### 핵심 언어 및 시스템
```text
주 사용 언어:  Rust (nightly 및 stable), Modern C++ (C++20 / C++23), ISO C (C11/C17)
보조 도구:     Go, Zig, Bash, Python (텔레메트리 분석 및 자동화 스크립트)
어셈블리:      x86_64 SIMD (AVX-512 / AVX2), 기초 ARM64 NEON 내장 함수
```

### 커널, I/O 및 네트워킹 서브시스템
| 영역 | 적용 기술 및 프레임워크 |
| :--- | :--- |
| **비동기 I/O** | `io_uring`, epoll, kqueue, 다이렉트 I/O (`O_DIRECT`), 비동기 파일 디스크립터 |
| **커널 관측성** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, 커널 트레이스포인트 |
| **동시성 제어** | 원자적 연산, 메모리 배리어, 락프리 링 버퍼, Hazard Pointers, RCU (Read-Copy Update) |
| **자료구조 토폴로지** | LSM-Tree, Bw-Tree, Skip List, Radix Tree, 원형 링 버퍼 |
| **디버깅 및 프로파일링** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 엔지니어링 철학

1. **기계적 공감 (Mechanical Sympathy)**  
   데이터의 물리적 배치가 성능을 결정합니다. 거짓 공유(False Sharing)를 방지하기 위해 구조체를 64바이트 캐시 라인 경계에 정확히 정렬하고, 포인터 추적(Pointer Chasing) 대신 순차적 메모리 접근 패턴을 지향하여 하드웨어 프리페처를 최대로 활용합니다.

2. **제로카피(Zero-Copy)의 원칙화**  
   핫 패스(Hot Path) 내부에서의 힙 할당은 설계 결함으로 간주합니다. 디스크나 네트워크 인터페이스로부터 메모리로 유입되는 모든 바이트는 운영체제 프리미티브가 허용하는 한 고정 메모리(Pinned Memory) 상에서 제로카피 버퍼를 통해 이동합니다.

3. **결정론적 장애 격리 (Deterministic Failure Domains)**  
   분산 시스템의 실패 모드는 복잡합니다. 취약한 휴리스틱 복구 로직에 의존하기보다, 명확한 상태 조정, 자체 치유 WAL 복구, 재현 가능한 카오스 엔지니어링 테스트를 거친 Crash-Only 소프트웨어 아키텍처를 추구합니다.

---

## 🖥️ 개발 환경

```text
운영체제:   Debian GNU/Linux (Sid / Testing) 및 Arch Linux (커스텀 zen 커널)
편집기:     Neovim (Lua 기반 경량 설정, rust-analyzer & clangd LSP 연동)
터미널:     Alacritty + tmux
셸:         zsh (최소화된 프롬프트 구성, vi-mode 활성화)
모니터:     듀얼 27인치 4K 디스플레이 (피벗 세로/가로 배치)
하드웨어:   AMD Ryzen 9 7950X (16코어 32스레드), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ 코드 너머의 일상

- **에스프레소 추출 동역학**: 플랫 버(Flat Burr) 그라인더의 미세 입도 세팅 및 튜닝된 듀얼 보일러 수동 레버 머신을 활용한 유량/압력 프로파일링.
- **모듈러 신디사이저 사운드 디자인**: 유로랙(Eurorack) 아날로그 모듈, 클록 디바이더, 스텝 시퀀서를 활용한 하드웨어 신호 패칭.
- **볼더링 & 알파인 등반**: 날씨와 일정이 허락할 때마다 스위스 알프스의 화강암 볼더와 암벽에서 균형을 찾습니다.

---

## 📬 연락처 및 공개 키

- **위치**: 스위스 취리히 (8005)
- **이메일**: `matteo.valenti.systems@gmail.com`
- **PGP 핑거프린트**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix**: `@mvalenti:matrix.org`
