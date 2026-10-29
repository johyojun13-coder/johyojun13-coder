| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [BR Português](./pt-BR.md) | [SA العربية](./ar.md) |

---

# Matteo Valenti

**Ingénieur Logiciel Systèmes & Développeur de Moteurs de Stockage**  
Basé à Zurich, Suisse · Originaire de Bologne, Italie  

> *"Sympathie mécanique (Mechanical Sympathy), E/S avec contournement du noyau et concurrence déterministe sur architectures massivement multicoeurs."*

Je conçois et développe des moteurs de stockage à très faible latence, des architectures d'E/S asynchrones et des primitives de journalisation distribuée. Mon travail s'articule autour des composants internes du noyau Linux, des structures de données concurrentes sans verrou (*lock-free*) et de la disposition de la mémoire adaptée au matériel. Lorsqu'une application s'interrompt en attente d'E/S ou gaspille des cycles d'horloge dans la contention de mutex, c'est précisément là que j'interviens.

---

## 🧭 Axes de Recherche et Chantiers Actuels

- **Moteurs d'Accès Direct NVMe** : Conception de `ring-kv`, un magasin clé-valeur embarqué expérimental articulé autour de Linux `io_uring` et de périphériques de blocs partitionnés par zones (ZBC/ZNS).
- **Journalisation en Amont (WAL) sans Verrou** : Réduction de la latence de queue d'écriture p99.9 dans les machines à états Raft grâce à des mémoires tampons circulaires et au traitement par lots vectorisé sans copie.
- **Télémétrie Système via eBPF** : Développement de sondes de traçage au niveau du noyau pour identifier la gigue d'ordonnancement et la saturation des interconnexions entre nœuds NUMA sur des charges intensives.
- **Rigueur des Micro-benchmarks** : Élaboration de suites de tests reproductibles pour l'évaluation des défauts de cache et des erreurs de prédiction de branchement dans les allocateurs de mémoire de bas niveau.

---

## 🛠️ Projets Open Source Phares

| Dépôt | Stack Technique | Statut | Description |
| :--- | :--- | :--- | :--- |
| **`ring-kv`** | Rust, C, Linux `io_uring` | Actif | Moteur de stockage clé-valeur LSM-tree asynchrone et embarqué supprimant la surcharge de bascule de contexte espace utilisateur/noyau. |
| **`wal-compact`** | Rust, SIMD | Maintenu | Sérialiseur de segments Write-Ahead Log sans copie avec validation CRC32 vectorisée et compactage concurrent de snapshots. |
| **`trace-sched`** | C, eBPF / BCC, Python | Maintenu | Suite de sondes d'observation Linux pour quantifier l'impact de la migration de threads et les invalidations de caches entre cœurs. |
| **`syn-drift`** | Go, POSIX Timers | Actif | Démon d'observation de haute précision mesurant les dérives temporelles d'horloges matérielles PTP/NTP à l'échelle de la microseconde. |

---

## 💻 Compétences Techniques & Environnement

### Langages et Fondations Systèmes
```text
Langages Principaux :  Rust (nightly et stable), C++ Moderne (C++20 / C++23), C Standard (C11/C17)
Outils Complémentaires : Go, Zig, Bash, Python (analyse de télémétrie et outillage)
Assembleur :           x86_64 SIMD (AVX-512 / AVX2), intrinsèques de base ARM64 NEON
```

### Sous-systèmes Noyau, E/S et Réseau
| Domaine | Technologies & Outils |
| :--- | :--- |
| **E/S Asynchrones** | `io_uring`, epoll, kqueue, E/S directes (`O_DIRECT`), descripteurs de fichiers asynchrones |
| **Observabilité Noyau** | eBPF, BCC, `bpftrace`, `perf`, `ftrace`, `strace`, points de trace du noyau |
| **Primitives de Concurrence** | Instructions atomiques, barrières de mémoire, tampons en anneau sans verrou, Hazard Pointers, RCU |
| **Topologies de Données** | Arbres LSM, Arbres Bw, Skip Lists, Arbres Radix, mémoires circulaires |
| **Débogage et Profilage** | GDB, Valgrind, AddressSanitizer (ASan), ThreadSanitizer (TSan), Hotspot, Coz |

---

## 📐 Principes d'Ingénierie

1. **Conception Adaptée au Matériel (Mechanical Sympathy)**  
   La disposition spatiale des données détermine la performance réelle. Les structures sont strictement alignées sur des lignes de cache de 64 octets pour éviter le faux partage (*false sharing*). Les accès séquentiels sont systématiquement privilégiés par rapport aux sauts de pointeurs pour maximiser le préchargement matériel.

2. **Le Zéro-Copie comme Règle Absolue**  
   L'allocation dynamique sur le chemin critique des données est considérée comme un défaut d'architecture. Tout octet provenant du disque ou du réseau est épinglé en mémoire et transféré via des tampons zéro-copie dès que le système d'exploitation l'autorise.

3. **Domaines de Défaillance Déterministes**  
   Les pannes des architectures distribuées sont non-linéaires. Je privilégie les architectures logicielles de type *crash-only* : une réconciliation claire des états, une récupération autonome via le journal (WAL) et des tests reproductibles d'ingénierie du chaos, plutôt que des heuristiques de récupération fragiles.

---

## 🖥️ Poste de Travail Quotidien

```text
Système d'exploitation : Debian GNU/Linux (Sid / Testing) et Arch Linux (noyau zen personnalisé)
Éditeur :                Neovim (configuration Lua minimale, LSP via rust-analyzer et clangd)
Terminal :               Alacritty + tmux
Shell :                  zsh avec invite épurée (mode vi activé)
Affichage :              Configuration double écran 4K 27 pouces (portrait et paysage)
Matériel :               AMD Ryzen 9 7950X (16 cœurs/32 threads), 64GB DDR5-6000 ECC, PCIe 4.0 NVMe RAID-0
```

---

## ☕ En Dehors du Code

- **Dynamique d'Extraction de l'Espresso** : Réglage micrométrique de moulins à meules plates et cartographie des profils de pression et de débit sur une machine manuelle à levier à double chaudière modifiée.
- **Synthèse Audio Modulaire** : Conception sonore matérielle sur synthétiseurs analogiques Eurorack, diviseurs d'horloge et séquenceurs pas-à-pas.
- **Bloc et Escalade Alpine** : Recherche d'adhérence sur le granite des Alpes suisses dès que la météo et les temps de compilation le concèdent.

---

## 📬 Contact & Clés Publiques

- **Localisation** : Zurich (8005), Suisse
- **Courriel** : `matteo.valenti.systems@gmail.com`
- **Empreinte PGP** : `4A1B 982E F03C 8D71 25BA 7390 CE45 8F12 B9A0 D214`
- **Matrix** : `@mvalenti:matrix.org`
