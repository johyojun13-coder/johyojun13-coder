| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [BR Português](./pt-BR.md) | [SA العربية](./ar.md) |

---

# Matteo Valenti

**Ingeniero de Software de Sistemas y Creador de Motores de Almacenamiento**  
Residente en Zúrich, Suiza · Originario de Bolonia, Italia  

> *"Simpatía mecánica (Mechanical Sympathy), I/O con bypass del kernel y concurrencia determinista en arquitecturas de alto conteo de núcleos."*

Diseño y construyo motores de almacenamiento de ultrabaja latencia, arquitecturas de E/S asíncrona y primitivas de registros distribuidos. La mayor parte de mi trabajo se sitúa en la intersección entre los componentes internos del kernel de Linux, las estructuras de datos concurrentes sin bloqueos (lock-free) y los diseños de memoria orientados al hardware. Cuando una aplicación se detiene en esperas de I/O o disipa ciclos de CPU en contención de mutex, es ahí donde intervengo.

---

## 🧭 Líneas de Investigación y Foco Actual

- **Motores de Acceso Directo NVMe**: Diseño de `ring-kv`, un almacén clave-valor embebido experimental construido sobre Linux `io_uring` y dispositivos de bloques zonificados (ZBC/ZNS).
- **Write-Ahead Logging sin Bloqueos**: Reducción de la latencia de cola p99.9 de escritura en máquinas de estados distribuidas Raft mediante búferes circulares en anillo y procesamiento por lotes sin copia vectorizado.
- **Telemetría de Sistemas con eBPF**: Desarrollo de sondas de rastreo dentro del kernel para diagnosticar el jitter del planificador y la saturación de interconexión entre nodos NUMA en cargas de trabajo de alto rendimiento.
- **Rigor en Microbenchmarking**: Creación de suites de pruebas reproducibles para fallos de caché (cache misses) y predicciones de saltos erróneas orientadas a asignadores de memoria de bajo nivel.

---

## 🛠️ Proyectos de Código Abierto Destacados

| Repositorio | Stack Tecnológico | Estado | Descripción |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | Activo | Motor de almacenamiento clave-valor LSM-tree asíncrono y embebido que suprime la sobrecarga del cambio de contexto entre usuario y kernel. |
| **`wal-compact`** | Rust, SIMD | Mantenido | Serializador de segmentos Write-Ahead Log de copia cero con verificación CRC32 vectorizada y compactación concurrente de instantáneas. |
| **`trace-sched`** | C, eBPF / BCC, Python | Mantenido | Conjunto de sondas ligeras de rastreo en Linux para identificar el coste de migración de hilos y las invalidaciones de caché entre núcleos. |
| **`syn-drift`** | Go, POSIX Timers | Activo | Demonio de monitorización de alta precisión para el análisis de desviaciones de reloj de hardware PTP/NTP a nivel de microsegundos. |

---

## 💻 Capacidades Técnicas y Herramientas

### Lenguajes y Sistemas Fundamentales
```text
Principales:    Rust (nightly y stable), C++ Moderno (C++20 / C++23), C Estándar (C11/C17)
Complementarios: Go, Zig, Bash, Python (análisis de telemetría y automatización)
Ensamblador:    x86_64 SIMD (AVX-512 / AVX2), intrínsecos básicos ARM64 NEON
```

### Subsistemas de Kernel, I/O y Redes
| Dominio | Tecnologías y Marcos |
| :--- | :--- |
| **E/S Asíncrona** | `io_uring`, epoll, kqueue, E/S directa (`O_DIRECT`), descriptores de archivo asíncronos |
| **Observabilidad del Kernel** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, puntos de traza del kernel |
| **Primitivas de Concurrencia** | Instrucciones atómicas, barreras de memoria, ring buffers lock-free, Hazard Pointers, RCU |
| **Topologías de Datos** | Árboles LSM, Árboles Bw, Skip Lists, Árboles Radix, búferes circulares |
| **Depuración y Perfilado** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 Principios de Ingeniería

1. **Diseño Consciente del Hardware (Mechanical Sympathy)**  
   La disposición física de los datos determina el rendimiento. Las estructuras se alinean estrictamente a límites de línea de caché de 64 bytes para evitar el falso intercambio (*false sharing*); se priorizan los patrones de acceso secuencial frente al salto de punteros para maximizar la eficacia del precargador de hardware.

2. **Copia Cero como Regla Inviolable**  
   Las asignaciones dinámicas de memoria dentro de la ruta crítica de datos se consideran fallos arquitectónicos. Cualquier byte transferido desde el almacenamiento o la red se fija en memoria (*pinned*) y se desplaza mediante búferes de copia cero siempre que las primitivas del sistema operativo lo permitan.

3. **Dominios de Fallo Deterministas**  
   Los sistemas distribuidos colapsan de formas complejas. Doy prioridad al paradigma *crash-only software*: reconciliación clara del estado, recuperación autónoma mediante WAL y pruebas rigurosas de caos reproducible, en lugar de heurísticas frágiles de recuperación.

---

## 🖥️ Entorno de Trabajo Diario

```text
Sistema Operativo: Debian GNU/Linux (Sid / Testing) y Arch Linux (kernel zen personalizado)
Editor:            Neovim (configuración ligera en Lua, LSP con rust-analyzer y clangd)
Terminal:          Alacritty + tmux
Shell:             zsh con indicador minimalista (modo vi activado)
Monitores:         Doble pantalla 4K de 27 pulgadas (disposición vertical y horizontal)
Hardware:          AMD Ryzen 9 7950X (16 núcleos/32 hilos), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ Fuera del Código

- **Dinámica de Extracción de Café Espresso**: Calibración micrométrica de molinos con muelas planas y seguimiento de curvas de flujo y presión en una máquina de palanca manual de doble caldera modificada.
- **Síntesis de Audio Modular**: Diseño de sonido y conexiones físicas con módulos analógicos Eurorack, divisores de reloj y secuenciadores por pasos.
- **Búlder y Escalada Alpina**: Buscando agarre en las paredes de granito de los Alpes suizos siempre que el clima y los tiempos de compilación lo permitan.

---

## 📬 Contacto y Claves Públicas

- **Ubicación**: Zúrich (8005), Suiza
- **Correo Directo**: `matteo.valenti.systems@gmail.com`
- **Huella Digital PGP**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix**: `@mvalenti:matrix.org`
