# Bomberman DOM

A real-time multiplayer Bomberman game with a Go WebSocket backend and a custom JavaScript mini-framework frontend.

## Features

- **Real-time Multiplayer**: 2-4 players via WebSocket connections
- **Game Lobby System**: 
  - Nickname input and validation
  - Waiting room with live player list
  - Group chat functionality
  - Smart timer logic (20s wait, then 10s countdown)
- **Game Logic** (Backend):
  - Player movement and collision detection
  - Bomb placement and explosions
  - Flame propagation system
  - Power-ups (speed, bomb count, range)
  - Win/lose conditions
  - Map generation with destructible/indestructible blocks
- **Responsive Design**: Modern UI that works on desktop and mobile

## Tech Stack

- **Backend**: Go 1.23+ with Gorilla WebSocket
- **Frontend**: Custom mini-framework with Virtual DOM (no external libraries)
- **Communication**: WebSocket protocol for real-time updates
- **Styling**: Pure CSS

**Frontend uses NO external frameworks** - only a custom mini-framework and vanilla JavaScript!

## Project Structure

```
bomberman-dom/
├── backend/                # Go backend
│   ├── game.go            # Core game loop and logic
│   ├── lobby.go           # Lobby and WebSocket handler
│   ├── player.go          # Player logic
│   ├── bomb.go            # Bomb mechanics
│   ├── map.go             # Map generation
│   ├── powerup.go         # Power-up system
│   ├── models/            # Data models and protocols
│   │   ├── models.go     # Game state structures
│   │   └── protocols.go  # WebSocket message formats
│   └── utils/             # Helper utilities
│       └── utils.go
├── mini-framework/         # Custom frontend framework
│   ├── App.js             # Main app class
│   ├── VirtualDom.js      # Virtual DOM implementation
│   ├── StateManager.js    # State management
│   ├── Routing.js         # Client-side routing
│   └── TodoDomUpdater.js  # DOM update utilities
### Prerequisites
- **Go 1.23+**: [Download here](https://go.dev/dl/)
- **Modern browser**: Chrome, Firefox, Safari, or Edge

### Steps

1. **Clone or navigate to the project directory**
   ```bash
   cd bomberman-dom
   ```

2. **Install Go dependencies**
   ```bash
   go mod download
   ```

3. **Start the backend server**
   ```bash
   go run main.go
   ```
   Server starts on `http://localhost:8080` with WebSocket endpoint at `ws://localhost:8080/ws/lobby`

4. **Open the game**
   - Navigate to `http://localhost:8080` in your browser
   - Open multiple browser tabs/windows to test multiplayer
   Architecture

### Backend (Go)
- **WebSocket Server**: Real-time bidirectional communication using Gorilla WebSocket
- **Game Loop**: Server-side game tick at ~60 FPS for smooth gameplay
- **State Broadcasting**: Pushes game state updates to all connected clients
- **Protocol**: JSON-based message format for client-server communication

### Frontend (Custom Framework)
- **Virtual DOM**: Efficient DOM updates with `createElement()` and diffing
- **State Management**: Reactive state updates trigger automatic re-renders
- **WebSocket Client**: Maintains connection, handles reconnection logic
- **Component System**: Functional components with unidirectional data flow

### Example Component:

```javascript
import { createElement } from './mini-framework/VirtualDom.js';

export function MyComponent(state, onAction) {
    return createElement('div', { className: 'my-component' },
        createElement('h1', {}, 'Hello World'),
        createElement('button', {
            onclick: () => onAction('clicked')
        }, 'Click Me')
    );
}
```

## Development

- **Backend**: Edit files in `backend/` and restart server
- **Frontend**: Edit files in `components/` or `mini-framework/`, refresh browser
- **Testing Multiplayer**: Open multiple browser tabs/windows

## Future Enhancements

- [ ] Game screen UI implementation  
- [ ] Sound effects and animations
- [ ] Leaderboard and statistics
- [ ] Multiple game rooms
- [ ] Spectator mode
- **State Management**: Centralized state with automatic UI updates
- **Component System**: Reusable UI components
- **Event Handling**: Declarative event binding
- **Routing**: Hash-based client-side routing

### Example Component:

```javascript
import { createElement } from './mini-framework/VirtualDom.js';

export function MyComponent(state, onAction) {
    return createElement('div', { className: 'my-component' },
        createElement('h1', {}, 'Hello World'),
        createElement('button', {
            onclick: () => onAction('clicked')
        }, 'Click Me')
    );
}
```

## UI Demo Features

- Simulated multiplayer experience
- Working chat with bot responses  
- Timer logic demonstration
- Responsive design showcase
- State management example

**This is a UI-only demonstration.** The actual game logic (board, movement, bombs) would be built on top of this foundation.
