| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [BR Português](./pt-BR.md) | [SA العربية](./ar.md) |

---

# Matteo Valenti

**Engenheiro de Software de Sistemas & Desenvolvedor de Motores de Armazenamento**  
Baseado em Zurique, Suíça · Natural de Bolonha, Itália  

> *"Simpatia mecânica (Mechanical Sympathy), E/S com bypass de kernel e concorrência determinística em arquiteturas com alta contagem de núcleos."*

Projeto e construo motores de armazenamento de ultrabaixa latência, arquiteturas de E/S assíncronas e primitivas de registros distribuídos. A maior parte do meu trabalho situa-se na interseção entre os componentes internos do kernel do Linux, estruturas de dados concorrentes sem bloqueio (*lock-free*) e layouts de memória conscientes do hardware. Quando uma aplicação trava em esperas de E/S ou queima ciclos de processamento em contenção de mutex, é aí que eu atuo.

---

## 🧭 Focos de Pesquisa e Atividades Recentes

- **Motores de Acesso Direto NVMe**: Projeto do `ring-kv`, um armazenamento chave-valor embarcado experimental construído em torno do Linux `io_uring` e dispositivos de blocos particionados por zonas (ZBC/ZNS).
- **Write-Ahead Logging sem Travamento**: Redução da latência de cauda p99.9 de gravação em máquinas de estados Raft distribuídas por meio de buffers em anel circulares e processamento em lote sem cópia vetorizado.
- **Telemetria de Sistemas com eBPF**: Desenvolvimento de sondas de rastreamento no kernel para diagnosticar *jitter* de escalonamento e saturação de nós NUMA sob cargas de trabalho extremas.
- **Rigor em Micro-benchmarks**: Criação de suítes de testes reproduzíveis para falhas de cache (*cache misses*) e erros de predição de desvios voltadas a alocadores de memória de baixo nível.

---

## 🛠️ Projetos de Código Aberto em Destaque

| Repositório | Stack Tecnológica | Status | Descrição |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | Ativo | Motor de armazenamento chave-valor LSM-tree assíncrono e embutido que elimina o overhead de troca de contexto entre usuário e kernel. |
| **`wal-compact`** | Rust, SIMD | Mantido | Serializador de segmentos Write-Ahead Log com cópia zero, verificação CRC32 vetorizada e compactação concorrente de snapshots. |
| **`trace-sched`** | C, eBPF / BCC, Python | Mantido | Conjunto de sondas leves de rastreamento no Linux para mapear custos de migração de threads e invalidação de cache entre núcleos. |
| **`syn-drift`** | Go, POSIX Timers | Ativo | Daemon de monitoramento de alta precisão para análise de desvio de relógio de hardware PTP/NTP na escala de microssegundos. |

---

## 💻 Habilidades Técnicas e Ferramentas

### Linguagens e Fundamentos de Sistemas
```text
Linguagens Principais:   Rust (nightly e stable), C++ Moderno (C++20 / C++23), ISO C (C11/C17)
Linguagens Auxiliares:   Go, Zig, Bash, Python (análise de telemetria e scripts de suporte)
Assembly:                x86_64 SIMD (AVX-512 / AVX2), intrínsecos básicos ARM64 NEON
```

### Subsistemas de Kernel, E/S e Redes
| Domínio | Tecnologias e Frameworks |
| :--- | :--- |
| **E/S Assíncrona** | `io_uring`, epoll, kqueue, E/S direta (`O_DIRECT`), descritores de arquivos assíncronos |
| **Observabilidade de Kernel** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, tracepoints do kernel |
| **Primitivas de Concorrência** | Instruções atômicas, barreiras de memória, buffers circulares lock-free, Hazard Pointers, RCU |
| **Topologias de Dados** | Árvores LSM, Árvores Bw, Skip Lists, Árvores Radix, buffers em anel |
| **Depuração e Perfilamento** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 Filosofia de Engenharia

1. **Design Consciente do Hardware (Mechanical Sympathy)**  
   O layout físico dos dados define o teto de desempenho. Estruturas são alinhadas estritamente a limites de linhas de cache de 64 bytes para evitar o falso compartilhamento (*false sharing*). Padrões de acesso sequencial são preferidos em relação a cadeias de ponteiros para maximizar o prefetcher de hardware.

2. **Cópia Zero como Regra Absoluta**  
   Alocações dinâmicas de memória no caminho crítico de processamento de dados são tratadas como falhas de projeto. Todo byte vindo do disco ou da placa de rede permanece em memória fixada (*pinned memory*) e trafega por buffers sem cópia sempre que o sistema operacional permitir.

3. **Domínios de Falha Determinísticos**  
   Sistemas distribuídos falham de maneiras complexas e não lineares. Priorizo a arquitetura de software *crash-only*: reconciliação de estado transparente, recuperação autônoma via WAL e testes reprodutíveis de caos, em vez de heurísticas frágeis de restauração.

---

## 🖥️ Estação de Trabalho Diária

```text
Sistema Operacional: Debian GNU/Linux (Sid / Testing) e Arch Linux (kernel zen personalizado)
Editor:              Neovim (configuração leve em Lua, LSP via rust-analyzer e clangd)
Terminal:            Alacritty + tmux
Shell:               zsh com prompt minimalista (modo vi habilitado)
Monitores:           Dois monitores 4K de 27 polegadas (configuração vertical e horizontal)
Hardware:            AMD Ryzen 9 7950X (16 núcleos/32 threads), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ Além do Terminal

- **Dinâmica de Extração de Espresso**: Calibração micrométrica de moinhos com lâminas planas e acompanhamento de gráficos de pressão e vazão em uma máquina manual de alavanca de caldeira dupla modificada.
- **Síntese Modular de Áudio**: Criação de timbres e experimentos acústicos usando módulos analógicos Eurorack, divisores de clock e sequenciadores por passos.
- **Bouldering e Escalada Alpina**: Buscando equilíbrio e concentração nas paredes de granito dos Alpes Suíços sempre que o tempo e os ciclos de compilação permitem.

---

## 📬 Contato e Chaves Públicas

- **Localização**: Zurique (8005), Suíça
- **E-mail Direto**: `matteo.valenti.systems@gmail.com`
- **Fingerprint PGP**: `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix**: `@mvalenti:matrix.org`
