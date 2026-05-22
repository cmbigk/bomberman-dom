# 🎮 Bomberman DOM - Real-Time Multiplayer Game

A premium, modern, fully-playable real-time multiplayer **Bomberman** game. This project features a low-latency concurrent **Go WebSocket Backend** and a highly responsive, custom-built **pure JavaScript Virtual DOM Mini-Framework Frontend**.

No heavy external libraries or UI frameworks (like React, Vue, or Tailwind) were used. The frontend is built entirely using vanilla JS and raw CSS to achieve state-of-the-art retro arcade styling, smooth micro-animations, and responsive glassmorphic interfaces.

---

## ✨ Features

### 🕹️ Interactive Gameplay Mechanics
- **Grid-Based Arena**: Classic 15x13 map layout constructed with indestructible boundary/pillar walls and destructible blocks.
- **Bomb Laying & Explosions**: Drop active bombs with ticking timers. Bricks explode, and players must dodge high-damage fire cells (`🔥`).
- **Hidden Power-Ups**: Destroy blocks to uncover and collect power-ups that enhance your capabilities:
  - 👟 **Speed Up**: Increases your movement speed.
  - 🔥 **Flame Up**: Boosts your bomb's explosion range.
  - 💣 **Bomb Up**: Elevates your maximum simultaneous bomb capacity.
- **Multiplayer State Sync**: High-frequency WebSocket updates synchronize player positions, active bombs, flame cells, and collected power-ups across all connected clients.
- **Victory & Defeat Logic**: Every player starts with **3 lives**. The last standing player wins! High-visibility overlay modals and victory banners display game-over results.

### 👥 Interactive Waiting Room & Lobby
- **Smart Queue Timers**: 
  - Dynamic **20-second wait timer** starts as soon as 2+ players join.
  - Quick **10-second starting countdown** triggers when the room is full (4 players) or the wait time expires.
- **Real-Time Lobby Chat**: Active text channel with message history, bot assistance, and concurrent connection support.

### 📊 Live Game HUD & Sidebar
- **Live Stats Panel**: Real-time HUD showing player statuses (Alive/Dead), remaining lives (`❤️`), bomb capacity (`💣`), and flame range (`🔥`).
- **Interactive Mini-Map**: Dynamic sidebar CSS grid mini-map replicating the live game state in real time.
- **Controls Reference Guide**: Persistent on-screen control helper mapping movement keys and precise actions.

---

## 🛠️ Tech Stack

### Frontend Architecture
- **Pure JavaScript Virtual DOM**: A bespoke virtual DOM engine (`mini-framework/`) providing:
  - **`VirtualDom.js`**: Memory-efficient diffing and patching (`createElement` / `updateDom`).
  - **`StateManager.js`**: Centralized single-source-of-truth state machine subscribing views to atomic changes.
  - **`Routing.js`**: Lightweight hash-based routing.
- **Styling**: Curated vanilla CSS (`styles.css`) establishing a glowing futuristic cyberpunk dashboard, fluid micro-transitions, retro arcade text shadows, and high-performance flex/grid layouts.

### Backend Architecture
- **Concurrent Go WebSocket Server** (`backend/`):
  - High-performance Go network stack (`net/http` & WebSocket handlers).
  - Centralized game loops, collision-detection engines, physics vectors, and message routers.
  - CORS-enabled with fully broadcast-safe lobby managers.

---

## 📂 Project Structure

```
bomberman-dom/
├── backend/                 # Concurrent Go WebSocket Backend
│   ├── models/              # Game schema definitions
│   ├── utils/               # Map generators and helper libraries
│   ├── main.go              # Backend entrypoint (listens on :8080)
│   ├── lobby.go             # Lobby session management
│   ├── game.go              # Game loop & win/lose logic
│   ├── player.go            # Player movement & physics
│   ├── bomb.go              # Bomb timing & blast calculations
│   └── powerup.go           # Power-up spawning & collision logic
├── mini-framework/          # Bespoke Virtual DOM UI Engine
│   ├── App.js               # Application coordinator
│   ├── VirtualDom.js        # Core tree creation and diffing
│   ├── StateManager.js      # Global state subscription
│   ├── Routing.js           # Client-side route dispatcher
│   └── domCleaner.js        # DOM hygiene utilities
├── components/              # UI View Components
│   ├── NicknameScreen.js    # Glassmorphic entry & nickname validator
│   ├── WaitingRoom.js       # Live chat and interactive queue
│   └── GameScreen.js        # Real-time game board, sidebar stats, and HUD
├── main.js                  # Frontend client entrypoint
├── gameState.js             # Client-side WebSocket network adapter
├── styles.css               # Premium CSS design tokens & animations
├── dev-server.js            # Pure Node.js development server (port 3000)
└── index.html               # Master HTML template
```

---

## 🚀 Installation & Getting Started

Follow these simple steps to run the Bomberman game locally.

### Prerequisites
- [Go](https://go.dev/doc/install) (version 1.18+ recommended)
- [Node.js](https://nodejs.org/) (for serving static frontend files)

### Step 1: Start the Go Backend Server
Navigate to the `backend` directory and launch the server:
```bash
cd backend
go run .
```
*The backend server will successfully start listening for WebSocket connections at `ws://localhost:8080/ws`.*

### Step 2: Start the Frontend Client Server
Open a new terminal window, return to the project root, and boot the static development server:
```bash
node dev-server.js
```
*The dev server will boot up on `http://localhost:3000`.*

### Step 3: Play!
1. Open `http://localhost:3000` in multiple browser tabs or distinct browser instances to simulate multiplayer.
2. Enter unique nicknames and watch them sync live in the waiting room lobby.
3. Once the timers tick down, dive into the classic retro game arena!

---

## 🎮 Game Controls

Ensure the game board container is focused by clicking on the board.

| Action | Control Key | Alternative / Modifier |
| :--- | :--- | :--- |
| **Move Up** | <kbd>W</kbd> | <kbd>▲ Up Arrow</kbd> |
| **Move Down** | <kbd>S</kbd> | <kbd>▼ Down Arrow</kbd> |
| **Move Left** | <kbd>A</kbd> | <kbd>◀ Left Arrow</kbd> |
| **Move Right** | <kbd>D</kbd> | <kbd>▶ Right Arrow</kbd> |
| **Precise Single Step** | <kbd>Shift</kbd> + <kbd>WASD / Arrows</kbd> | *Aligns player perfectly to grid intersection* |
| **Place Bomb** | <kbd>SPACEBAR</kbd> | *Spawns bomb at player's active grid square* |

---



