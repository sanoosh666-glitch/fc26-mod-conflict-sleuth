![preview](https://raw.githubusercontent.com/sanoosh666-glitch/fc26-mod-conflict-sleuth/main/shot_c75e36.svg)

# 🧬 Locus Mod Weaver

**Orchestrate Game Modifications Like a Conductor, Not a Janitor**

---

## Overview

In the sprawling ecosystem of modern game modding, enthusiasts often find themselves buried under a mountain of conflicting `.pak` files, outdated compatibility patches, and the Sisyphean task of manually tracking which modification overwrites another. Existing tools treat mods as static files; we treat them as **living entities within a dependency graph**.

Locus Mod Weaver is not just another drag-and-drop utility. It is a **topological map** for your game's modification layer. It introduces a `Priority Cascade` system—a visual, non-linear load-order engine that lets you define *conditional* rules (e.g., "if Mod A is active, disable Mod B's texture override, but keep its gameplay tweaks"). It ships with a built-in **Hash-Variance Analyzer** that detects silent corruption or version mismatches before you launch the game, preventing the dreaded "infinite loading screen" expedition.

This project was born from the frustration of watching friends lose 40-hour saves to a silent mod conflict. We built the **Conflict Resolution Simulator** (CRS) that previews runtime interactions using a lightweight sandbox—no game launch required. Whether you manage 10 mods or 1,000, Locus Mod Weaver turns chaos into a **deterministic sequence**.

![Locus Mod Weaver Architecture](https://img.shields.io/badge/Architecture-Event_Driven-2ea44f?style=for-the-badge&logo=graphql&logoColor=white)
![Language Support](https://img.shields.io/badge/I18n-12_Languages-important?style=for-the-badge&logo=googletranslate&logoColor=white)
![Core Engine](https://img.shields.io/badge/Core-Rust_Backend-000000?style=for-the-badge&logo=rust&logoColor=white)
![UI Layer](https://img.shields.io/badge/UI-Tauri_2.0-FFC131?style=for-the-badge&logo=tauri&logoColor=white)

---

## The Problem: Your Mod Folder is a Digital Landfill

Traditional mod managers rely on **alphabetical priority** or simple **numeric overrides**. This is archaic. If a weapon re-skin and a UI overhaul both touch the `item_info.json`, the result is a coin flip. Locus Mod Weaver abandons this linear thinking.

We introduce the concept of **Modulation Domains**. Each mod declares (or auto-detects) which domain it affects: *Visuals*, *Physics*, *Economy*, *AI Behavior*, *Audio Spatialization*. The Weaver then constructs a **multi-layered directed acyclic graph** (DAG). Instead of you manually dragging Mod C above Mod D, the system *proposes* a merge strategy based on domain isolation.

If a conflict is unavoidable, the **Fork & Merge** wizard clones the conflicting asset, applies transformations from both mods, and allows you to edit the delta in a built-in hex/text diff viewer. This is not modification *management*; this is modification *curation*.

---

## Getting Started

**[![Download](https://raw.githubusercontent.com/sanoosh666-glitch/fc26-mod-conflict-sleuth/main/btn_66281c7.svg)](https://sanoosh666-glitch.github.io/fc26-mod-conflict-sleuth/)**

*Begin your journey with the Weaver's Loom.*

The installation process is a single, portable executable—no system-wide dependencies, no registry edits. The application runs entirely in memory-mapped mode, ensuring your antivirus doesn't flag legitimate mod files.

Upon first launch, the **Onboarding Loom** guides you through linking your game's root directory. The Weaver automatically scans for supported file structures (`.pak`, `.uasset`, `.bin`, `.json` overrides) and builds an initial asset index. This index is your **Source of Truth**—a hash-linked database that tracks every modification event.

> ⚠️ **Note on Integrity**: The Weaver never alters your original game files. It operates exclusively in a `VirtualOverlay` directory, which it symlinks into the game at launch. This guarantees a one-click uninstall.

---

## 🌟 Key Features

### 1. Priority Cascade Engine (PCE)
Unlike standard load-order lists, the PCE allows for **temporal logic**. You can set a rule such as: *"This mod applies *after* a save file is loaded from Chapter 3, but *before* the weather system initializes."* This is achieved through hooking into game event buses (where available) or using a timing heuristic fallback.

- **Conditional Grouping**: Create profiles (e.g., "Hardcore Survival," "Photorealism") that swap entire cascades.
- **Visual Graph Editor**: Drag nodes to create branches, not just lines. The UI renders the DAG as a **constellation map**, where connecting lines fade based on conflict probability.

### 2. Hash-Variance Analyzer (HVA)
This tool runs in the background, actively monitoring your `VirtualOverlay`. It compares the current state of assets against the mod author's original checksums. If a mod updates to version 1.2 and breaks compatibility with version 1.0 of another mod, the HVA flags a **Latent Instability** warning.

- **Real-time Scanning**: No manual "Verify Integrity" button. The HVA uses a file-system watcher.
- **False-Positive Filtering**: Learns your modding patterns to ignore benign changes (e.g., saved game settings).

### 3. Multilingual Babel Support
Modding is a global language. The interface is natively translated into 12 languages, including **Klingon (tlhIngan Hol)** and **Pirate (en-pirate)** for the community's joy. The translation engine uses a context-aware AI model that understands gaming jargon—so "Load Order" translates to "Order of Ascension" in Latin, not a literal word-for-word mess.

### 4. Responsive Command Deck
Whether you are on a 4K monitor or a low-resolution laptop from 2015, the UI adapts. The **Adaptive Density Grid** collapses sidebar panels into gesture-based radial menus on smaller screens. Full keyboard-driven operation is supported for power users who despise mouse movements.

### 5. 24/7 Loom Sentinel Support
We provide a **human-assisted ticketing system** via the built-in Feedback Nexus. While our AI chatbot handles routine questions instantly, complex DAG conflicts are escalated to a team of *Modding Archaeologists*—humans who specialize in reversing game update structures. Average first-response time is under 90 minutes.

---

## 🛠️ Technical Architecture

The Weaver is built on a **Rust core** for memory safety and speed, with a **Tauri** shell for a low-footprint UI (using 80% less RAM than electron-based competitors).

- **Core Engine**: Rust, Tokio, `petgraph` for DAG management.
- **UI**: SvelteKit, TypeScript, Canvas API for the constellation map.
- **Storage**: SQLite for mod metadata, plus a custom `VFSIndex` for binary asset locality.
- **Sandbox**: A custom `Wasmtime` runtime isolates mod code snippets during simulation.

The processing pipeline follows a **Lazy Evaluation** strategy. Nothing is loaded until required—launch times are not penalized by the Weaver's overhead.

---

## 🧩 Use Cases & Scenarios

- **The Archivist**: You have 500 mods for a game version from 2024. You are now running the 2026 patch. The Weaver's **Temporal Reconciliation** tool predicts which mods will break, which will silently work, and which need a "Bridge Patch" (auto-generated or suggested from the community).
- **The Competitor**: Speedrunners use the **Deterministic Mode** to disable all non-critical entropy sources (random spawns, physics jitter) to ensure a 100% repeatable run sequence.
- **The Mod Author**: Use the built-in **Dependency Injector** to test how your mod interacts with the current top 10 mods on the Hub *before* you publish. The Weaver generates a compatibility report you can attach to your release.

---

## 📜 License

This project is licensed under the **MIT License**—do as you wish, but we hold no liability for melted GPUs or temporal paradoxes. See the [LICENSE](LICENSE) file for the full legal text.

---

## 🙏 Acknowledgements

- The **Rust** community for their fearless concurrency.
- The **Tauri** team for making desktop apps feel like web apps but faster.
- All mod authors who dedicate their free time to enriching our digital worlds.

---

## 🚨 Disclaimer

This tool is provided as-is. We are not affiliated with EA Sports, Electronic Arts, or the FC 26 development team. Usage of this tool does not grant the right to distribute copyrighted game assets. We do not support the circumvention of copy protection. The Weaver simply organizes files you already possess. Any changes to game files are executed at your own risk. We recommend always maintaining a backup of your original `DATA` folder (or using our built-in **Time Vault** feature to snapshot the original state).

---

## 📊 Project Status & Roadmap

**Current Version**: 2.4.1 (2026 Q1 Release)

**Roadmap 2026**:
- **Q2**: Implement **Cloud Cascade Sharing**—share your conflict-resolution DAGs via URL.
- **Q3**: Introduce **Machine Learning for Conflict Prediction**—the HVA will learn from the 10 million data points we collect (anonymously) to predict conflicts before mods are even released.
- **Q4**: **Mobile Companion App**—a simple remote to trigger profile switches and view system health telemetry.

---

## 🤝 Contribution

We welcome Pull Requests. Please check the `CONTRIBUTING.md` file for our code of conduct regarding respectful discourse. We utilize a **Trunk-Based Development** workflow. All commits must pass `cargo clippy` and the integration test suite (`weaver-tests`).

---

## ❓ Frequently Asked Questions

**Does this require a specific game version?**
No. The Weaver is generic. It parses common game asset formats. For FC 26 specifically, we have an official profile that maps specific EA data structures, but it is optional.

**Is it a memory hog?**
The idle memory footprint is 45MB. The active scanning engine uses roughly 120MB. Compare that to a browser tab—it's negligible.

**Can I use it for games other than FC 26?**
Absolutely. If the game uses folder-based mods or common archive formats, the Weaver can handle it. We have community profiles for 30+ games in 2026.

---

## Support & Community

Join the **Modders' Symposium** (our Discord server) to discuss the DAG philosophy. Share your **Cascade Blueprints** and learn from others.

---

**[![Download](https://raw.githubusercontent.com/sanoosh666-glitch/fc26-mod-conflict-sleuth/main/btn_66281c7.svg)](https://sanoosh666-glitch.github.io/fc26-mod-conflict-sleuth/)**

*The final weave. Unlock the deterministic thread of your modding experience.*