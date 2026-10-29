| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# Matteo Valenti

**Leitender Systemsoftware-Ingenieur & Speicherarchitekt**  
Wohnhaft in Zürich, Schweiz · Geboren in Bologna, Italien  

> *"Mechanische Sympathie (Mechanical Sympathy), Kernel-Bypass-I/O und deterministische Nebenläufigkeit auf hochgradig parallelen Mehrkernsystemen."*

Ich entwerfe und implementiere latenzkritische Speicher-Engines, asynchrone I/O-Architekturen und verteilte Protokollierungs-Primitive. Der Schwerpunkt meiner Arbeit liegt an der Schnittstelle von Linux-Kernel-Interna, sperrenfreien (lock-free) parallelen Datenstrukturen und hardwarenahen Speicherlayouts. Wenn Anwendungen im I/O-Wait blockieren oder CPU-Zyklen in Mutex-Konflikten vergeuden, analysiere und behebe ich die Ursachen auf Systemebene.

---

## 🧭 Forschungsschwerpunkte & Aktuelle Arbeiten

- **NVMe-Direktzugriffs-Engines**: Entwicklung von `ring-kv`, einem experimentellen, eingebetteten Key-Value-Store auf Basis von Linux `io_uring` und zonierten Blockgeräten (ZBC/ZNS).
- **Sperrenfreies Write-Ahead-Logging**: Minimierung der p99.9-Schreiblatenz in verteilten Raft-Zustandsmaschinen durch zirkuläre Ringpuffer und vektorisierte Zero-Copy-Batchverarbeitung.
- **eBPF-basierte Systemtelemetrie**: Implementierung von Kernel-Tracing-Sonden zur Erkennung von Scheduler-Jitter und Interconnect-Engpässen zwischen NUMA-Knoten unter Hochlast.
- **Präzises Mikro-Benchmarking**: Aufbau reproduzierbarer Testumgebungen für Cache-Miss- und Branch-Misprediction-Analysen moderner Speicherallokatoren.

---

## 🛠️ Ausgewählte Open-Source-Projekte

| Repository | Technologie-Stack | Status | Beschreibung |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | Aktiv | Asynchrone, eingebettete LSM-Tree-Speicher-Engine ohne Kontextwechsel-Overhead zwischen Userspace und Kernel. |
| **`wal-compact`** | Rust, SIMD | Gepflegt | Zero-Copy-Serialisierer für Write-Ahead-Log-Segmente mit vektorisierter CRC32-Prüfung und paralleler Snapshot-Kompaktierung. |
| **`trace-sched`** | C, eBPF / BCC, Python | Gepflegt | Leichtgewichtige Tracing-Werkzeuge zur genauen Erfassung von Thread-Migrationskosten und kernübergreifender Cache-Invalidierung. |
| **`syn-drift`** | Go, POSIX Timers | Aktiv | Hochpräziser Dämon zur Messung und Überwachung von PTP/NTP-Hardware-Uhrenabweichungen im Mikrosekundenbereich. |

---

## 💻 Technische Fähigkeiten & Werkzeuge

### Kernsprachen & Systemschnittstellen
```text
Hauptsprachen:     Rust (nightly & stable), Modernes C++ (C++20 / C++23), ISO C (C11/C17)
Ergänzungen:       Go, Zig, Bash, Python (für Telemetrieanalysen und Tooling)
Assembler:         x86_64 SIMD (AVX-512 / AVX2), elementare ARM64 NEON Intrinsics
```

### Kernel-, I/O- & Netzwerk-Subsysteme
| Bereich | Technologien & Werkzeuge |
| :--- | :--- |
| **Asynchrone I/O** | `io_uring`, epoll, kqueue, direktes I/O (`O_DIRECT`), asynchrone Datei-Deskriptoren |
| **Kernel-Beobachtbarkeit** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, Kernel-Tracepoints |
| **Nebenläufigkeits-Primitive**| Atomare Befehle, Speicherbarrieren, sperrenfreie Ringpuffer, Hazard Pointers, RCU |
| **Datenstrukturen** | LSM-Bäume, Bw-Bäume, Skip-Listen, Radix-Bäume, zirkuläre Ringpuffer |
| **Debugging & Profiling** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 Technische Prinzipien

1. **Hardware-Bewusstes Design (Mechanical Sympathy)**  
   Die physikalische Anordnung der Daten im Speicher bestimmt die Systemleistung. Datenstrukturen werden strikt an 64-Byte-Cache-Line-Grenzen ausgerichtet, um False Sharing zu eliminieren. Sequenzielle Speicherzugriffe werden gegenüber Zeigerketten bevorzugt, um Hardware-Prefetcher optimal auszulasten.

2. **Zero-Copy als Grundsatz**  
   Dynamische Speicherallokationen im kritischen Datenpfad gelten als Architekturfehler. Jedes Byte, das von Festplatten oder Netzwerkschnittstellen eingelesen wird, verbleibt im gepinnten Speicher und wird ohne Kopiervorgänge verarbeitet, sobald das Betriebssystem dies ermöglicht.

3. **Deterministische Fehlerdomänen**  
   Verteilte Systeme scheitern auf unvorhersehbare Weise. Ich verfolge konsequent Crash-Only-Softwareprinzipien: präzise Zustandsabgleiche, selbstreparierende Protokollwiederherstellung und deterministische Chaos-Tests statt anfälliger, heuristischer Reparaturroutinen.

---

## 🖥️ Arbeitsumgebung

```text
Betriebssystem: Debian GNU/Linux (Sid / Testing) & Arch Linux (angepasster Zen-Kernel)
Editor:         Neovim (minimalistisches Lua-Setup, LSP via rust-analyzer & clangd)
Terminal:       Alacritty + tmux
Shell:          zsh mit schlanker Prompt-Konfiguration (vi-mode aktiviert)
Bildschirme:    Zwei 27-Zoll-4K-Displays (Pivot-Setup: Hochformat & Querformat)
Hardware:       AMD Ryzen 9 7950X (16 Kerne/32 Threads), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ Abseits des Terminals

- **Physik der Espresso-Extraktion**: Feinjustierung von Scheibenmahlwerken und Druck-/Durchfluss-Profilierung an einer modifizierten Zweikreiser-Handhebelmaschine.
- **Modulare Klangsynthese**: Schaltungs- und Signalexperimente mit analogen Eurorack-Synthesizermodulen, Clock-Dividern und Step-Sequenzern.
- **Bouldern & Alpinsport**: Wann immer das Wetter und die Rechenzeit es erlauben, suche ich den Ausgleich an den Granitwänden der Schweizer Alpen.

---

## 📬 Kontakt & Öffentliche Schlüssel

- **Standort**: Zürich (8005), Schweiz
- **E-Mail**: `matteo.valenti.systems@gmail.com`
- **PGP-Fingerabdruck**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix**: `@mvalenti:matrix.org`
