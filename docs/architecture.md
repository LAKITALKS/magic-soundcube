# Magic Soundcube – Architecture Overview

> Magic Soundcube is an interactive audio-puzzle in which players reconstruct a song by discovering the correct sequence of sounds on a 3-D cube.  
> Each cube face hosts a distinct audio layer (drums, melody, vocals, ambience, …).

---

## 1 · System Overview (modular & extendable)

| Layer            | Current Tech (prototype)           | Notes / Options             |
|------------------|------------------------------------|-----------------------------|
| **UI / UX**      | Lovable (no-code)                  | Replaceable by React + WebGL/WebAudio |
| **Audio Engine** | HTML5 Audio                        | WebAudio API planned for advanced mixing |
| **Puzzle Logic** | Client-side JS module              | Validates order, handles Undo & Hint     |
| **Data Layer**   | — *(planned)*                      | Firebase / Supabase for progress & scores|
| **Versioning**   | GitHub                             | GitHub Actions for CI/CD                 |

---

## 2 · Key Components

### Frontend
* Interactive 3-D cube (click / touch).
* Control bar: **Play All · Undo · Reset · Hint**.

### Audio Engine
* Maps each tile to a sample buffer.
* Records play-order; replays sequences on demand.
* Lightweight client-only implementation; switchable to server-rendered stems.

### Puzzle Logic
* Compares user sequence with solution array.
* Hint system reveals the next correct tile.
* Undo removes the last input step.

### Data Layer (planned)
* User sessions, high scores, custom challenges.
* Optional Firebase rules for privacy-friendly storage.

---

## 3 · Component Diagram

```mermaid
graph TD
  UI["UI – Soundcube"] -->|triggers| Audio["Audio Engine"]
  UI --> Logic["Puzzle Logic"]
  Logic --> Order[(Play Order)]
  Logic --> Hint[(Hint Module)]
  Logic --> Undo[(Undo Module)]
  Audio --> Assets[(Sound Assets)]
