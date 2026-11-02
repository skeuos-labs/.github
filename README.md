<p align="center">
  <img src="https://raw.githubusercontent.com/skeuos-labs/.github/main/profile/assets/skeuos-labs-symbol.png" width="128" height="128" alt="Skeuos Labs Symbol" />
</p>

<h1 align="center">Skeuos Labs</h1>

<p align="center">
  <strong>Modern, open-source software for the global church, worship teams, and AV production crews.</strong>
</p>

<p align="center">
  <a href="#ecosystem-architecture">Architecture</a> •
  <a href="#product-catalog--ecosystem-roster">Product Catalog</a> •
  <a href="#ecosystem-maturity-matrix">Maturity Matrix</a> •
  <a href="#engineering-values">Engineering Values</a>
</p>

<p align="center">
  <sub><em>"If anyone cleanses himself from what is dishonorable, he will be a vessel for honor, sanctified, useful to the Master, prepared for every good work."</em> — <strong>2 Timothy 2:21</strong></sub>
</p>

---

**Skeuos Labs** (*skeu-os*, Greek: **σκεῦος** — *vessel, tool, sacred instrument*) builds modern, open-source software for the global church, worship teams, and AV production crews.

We combine ancient worship heritage with modern software engineering: modular, high-performance, beautiful tools built to serve the gathered assembly.

---

## Ecosystem Architecture

All products in the ecosystem are independent repositories connected through shared domain libraries and open protocols. No monolithic lock-in.

```text
                             ┌────────────────────────┐
                             │  @skeuos-labs/mizmor   │
                             │   Presentation Engine  │
                             │  (Canonical AST/Types) │
                             └───────────┬────────────┘
                                         │
                 ┌───────────────────────┼───────────────────────┐
                 ▼                       ▼                       ▼
          ┌─────────────┐         ┌─────────────┐         ┌─────────────┐
          │   TARGUM    │         │   YACHAD    │         │    TAXIN    │
          │ Presentation│         │ Lyrics Sync │         │  ChurchOS   │
          │  Converter  │         │ & Matching  │         │ Management  │
          └──────┬──────┘         └─────────────┘         └──────┬──────┘
                 │                                               │
                 │              ┌─────────────┐                  │
                 └─────────────►│    SEMA     │◄─────────────────┘
                                │ AV Cue Sync │
                                │ (OSC/MIDI)  │
                                └─────────────┘

       ─────────────────────────────────────────────────────────────
                   Congregation & Worship Team Companions
       ─────────────────────────────────────────────────────────────
                ┌─────────────┐                 ┌─────────────┐
                │    SELAH    │                 │    ZAMAR    │
                │Sermon Notes │                 │  Musician   │
                │   & Bible   │                 │  Rehearsal  │
                └─────────────┘                 └─────────────┘
```

---

## Product Catalog & Ecosystem Roster

### Core Infrastructure

#### 1. Mizmor (`@skeuos-labs/mizmor`)
- **Soul Name:** Hebrew **מִזְמוֹר** (*mizmor*) — A psalm arranged with musical notation and meter.
- **Biblical Anchor:** Appears 57 times in the Psalms superscriptions (e.g. Psalm 23:1 *Mizmor l'David*).
- **Role:** Pure TypeScript presentation engine. Provides canonical presentation AST, round-trip format decoders and encoders (ProPresenter 6/7, VideoPsalm, FreeShow, PowerPoint, Plain Text), transcoders, and validation diagnostics.
- **Status:** **Active / Shipped (v1.0.0)** — Extracted into standalone repo with 432 automated tests.
- **Tech Stack:** `[Locked]` TypeScript (NodeNext / ESM), Vitest, Zod, Protobuf.js, fast-xml-parser, @zip.js. Zero UI or platform dependencies.

---

### Presentation & AV Ecosystem

#### 2. Targum
- **Soul Name:** Aramaic / Hebrew **תַּרְגּוּם** (*targum*) — Spoken translation of sacred text into the vernacular tongue so the assembly understands.
- **Biblical Anchor:** Ezra 4:7 (*u-m’turgam*), Nehemiah 8:8 (*"They read from the Book... making it clear and giving the sense, so that the people understood"*).
- **Role:** High-performance desktop conversion utility. Inspects, validates, visualizes, and converts presentation files across formats with rich slide review, diagnostics, and batch processing.
- **Status:** **Active / Shipped** — Desktop GUI complete with 131 tests passing.
- **Tech Stack:** `[Locked]` Tauri 2 (Rust), React 19, TypeScript, Vite, Tailwind CSS v4, Base UI, Zustand.

#### 3. Yachad
- **Soul Name:** Hebrew **יַחַד** (*yachad*) — Together as one; unity in voice and purpose.
- **Biblical Anchor:** Psalm 133:1 (*"How good and pleasant it is when brothers dwell together as one [yachad]"*), Isaiah 52:8 (*"Together they sing for joy"*).
- **Role:** Worship presentation synchronization agent. Watches local presentation directories, reconciles library differences between applications (e.g. ProPresenter ↔ VideoPsalm), detects missing songs, and syncs across computers, web, and mobile.
- **Status:** **Next in Queue (Design Phase)**.
- **Tech Stack:** `[Proposed - High Confidence]` Tauri (Rust background file watcher + system tray), TypeScript, `@skeuos-labs/mizmor`.

#### 4. Sema
- **Soul Name:** Greek **σῆμα** (*sēma*) — A signal, mark, cue, or prearranged token.
- **Biblical / Ancient Root:** Root of *semaphore*. Prearranged cue signaling AV equipment.
- **Role:** Live production automation bridge. Translates slide changes and presenter events into hardware control cues across OSC, MIDI, ProPresenter REST/WebSocket API, Art-Net/DMX lighting, and PTZ camera protocols.
- **Status:** **Roadmap / Concept**.
- **Tech Stack:** `[Open / Exploratory]` Rust daemon or Node.js lightweight background process; multi-protocol adapter architecture.

---

### Worship Life & Congregation Companions

#### 5. Selah
- **Soul Name:** Hebrew **סֶלָה** (*selah*) — Pause, lift up, meditate, reflect on the Word.
- **Biblical Anchor:** Appears 74 times in Scripture (71 times in Psalms, 3 in Habakkuk 3).
- **Role:** Mobile sermon note-taking and Bible companion app. Allows congregation members to follow along, capture notes with inline scriptures, audio/photo attachments, and sermon organization (multilingual: Malagasy, English, French). Tagline: *“Stay in the Word. Stay in the moment.”*
- **Status:** **Design / Mobile Prototype**.
- **Tech Stack:** `[Proposed - High Confidence]` React Native / Expo, TypeScript, SQLite / offline-first sync.

#### 6. Zamar
- **Soul Name:** Hebrew **זָמַר** (*zamar*) — To strike strings, make instrumental music, play skillfully in praise.
- **Biblical Anchor:** Psalm 33:2 (*"Make music [zamru-lo] on the ten-stringed lyre"*), Psalm 57:7, Psalm 144:9.
- **Role:** Musician-specific note-taking and rehearsal preparation app. Captures song arrangement reminders, chord cues, transpositions, and instrument notes tied directly to service setlists and ChurchOS service plans.
- **Status:** **Roadmap / Specification**.
- **Tech Stack:** `[Open / Exploratory]` Mobile/Tablet-first React Native / Expo or PWA.

---

### Church Management Hub

#### 7. Taxin
- **Soul Name:** Greek **τάξιν** (*taxin*, from τάξις) — Order, arrangement, proper structure.
- **Biblical Anchor:** 1 Corinthians 14:40 (*"Let all things be done decently and in order [kata taxin]"*).
- **Role:** Core church coordination platform. Church and campus management, member directories, team scheduling, service planning, and song playlist building with slide previews powered by `@skeuos-labs/mizmor`.
- **Status:** **Roadmap / Architecture Design**.
- **Tech Stack:** `[Open / Exploratory]` Modern TypeScript full-stack web application (framework TBD), PostgreSQL, REST/GraphQL API.

---

## Ecosystem Maturity Matrix

| Product / Package | Role | Current Status | Primary Language | License |
|---|---|---|---|---|
| **`@skeuos-labs/mizmor`** | Presentation Engine | **v1.0.0 Shipped** | TypeScript | MIT |
| **`Targum`** | Desktop Converter | **v0.1.0 Shipped** | Rust / TypeScript | MIT |
| **`Yachad`** | Song & Lyrics Sync | **Next in Queue** | Rust / TypeScript | MIT |
| **`Selah`** | Sermon Notes & Bible | **Design Phase** | TypeScript (React Native) | MIT |
| **`Zamar`** | Rehearsal Notes | **Roadmap** | TypeScript | MIT |
| **`Taxin`** | Church Core Platform | **Roadmap** | TypeScript | MIT |
| **`Sema`** | AV Hardware Bridge | **Roadmap** | Rust / TypeScript | MIT |

---

## Engineering Values

1. **Craft As Worship**: Code written for the church should reflect excellence in craftsmanship, test coverage, and documentation.
2. **Open Source & Permissive**: All core projects are MIT-licensed. No walled gardens or vendor lock-in for church data.
3. **Respect for Privacy & Sacred Space**: Congregation and church data belongs to the local assembly. Local-first architectures preferred wherever feasible.
4. **Community Collaboration**: Designed for contributors worldwide — whether fixing a format dialect, translating a language, or adding a hardware protocol.

---

<p align="center">
  <sub>Skeuos Labs • Soli Deo Gloria</sub>
</p>
