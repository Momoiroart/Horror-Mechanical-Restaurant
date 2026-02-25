# Project Structure - Mechanical Restaurant Horror

## Folder Organization (Roblox Studio)

```
📁 Workspace
├── 📁 Environment
│   ├── Lobby
│   │   ├── SpawnPoint
│   │   ├── UIPlates
│   │   └── TeleportPad
│   └── Restaurant
│       ├── Kitchen
│       ├── DiningArea
│       ├── Counter
│       ├── Windows (lockable)
│       └── ExitDoor (for challenge)
│
├── 📁 NPCs
│   ├── Customers
│   │   ├── NormalCustomer (R6)
│   │   └── WeirdCustomer (R6)
│   └── MechanicalAnimals
│       ├── AnimalVariant1
│       └── AnimalVariant2
│
├── 📁 Scripts (Server)
│   ├── GameManager
│   ├── LobbyManager
│   ├── CustomerManager
│   ├── FoodSystem
│   ├── CombatSystem
│   ├── NightManager
│   ├── WindowSystem
│   ├── ChallengeManager
│   ├── ProgressionSystem
│   └── DataStore (optional)
│
├── 📁 Scripts (Client)
│   ├── UIManager
│   ├── ClientInput
│   └── LocalEffects
│
├── 📁 ReplicatedStorage
│   ├── Shared
│   │   ├── Constants
│   │   ├── RemoteEvents
│   │   └── UtilityFunctions
│
├── 📁 ServerStorage
│   ├── Assets
│   │   ├── Models
│   │   └── Animations
│   └── Templates
│
└── 📁 Sound
    ├── Music
    └── SFX
```

---

## Key Scripts Overview

### Server Scripts

| Script | Purpose |
|--------|---------|
| `GameManager` | Main state machine (lobby → playing → night → day → ...) |
| `LobbyManager` | Handle join requests, player count, settings |
| `CustomerManager` | Spawn customers, assign orders, weird customer logic |
| `FoodSystem` | Recipes, cooking times, serving |
| `CombatSystem` | Kill button, weapons, damage |
| `NightManager` | Spawn mechanical animals, track aggression |
| `WindowSystem` | Lock/unlock state for each window |
| `ChallengeManager` | Track food disposal task completion |
| `ProgressionSystem` | Day count, gems, upgrade unlocks |

### Client Scripts

| Script | Purpose |
|--------|---------|
| `UIManager` | All GUI frames, buttons, HUD |
| `ClientInput` | Mouse clicks, keybinds |
| `LocalEffects` | Jumpscare, screen effects |

---

## RemoteEvents (ReplicatedStorage)

```
📁 RemoteEvents
├── RequestStartGame      (Client → Server)
├── CustomerOrdered       (Server → Client)
├── ServeFood             (Client → Server)
├── KillCustomer          (Client → Server)
├── ToggleWindow          (Client → Server)
├── CompleteChallenge     (Server → Client)
├── UpdateDay             (Server → Client)
├── UpdateGems            (Server → Client)
├── TriggerJumpscare      (Server → Client)
└── GameOver              (Server → Client)
```

---

## Suggested Naming Conventions

- **Scripts:** PascalCase (`GameManager`, `CustomerManager`)
- **Variables:** camelCase (`currentDay`, `isWeirdCustomer`)
- **Constants:** UPPER_SNAKE_CASE (`MAX_PLAYERS`, `DAY_DURATION`)
- **Events:** PascalCase with "Event" suffix (`CustomerOrderedEvent`)
- **Folders:** PascalCase (`Scripts`, `NPCs`, `Environment`)

---

## Quick Start Checklist

- [ ] Create all folders
- [ ] Add placeholder parts for environment
- [ ] Create 1 NPC placeholder
- [ ] Set up 1 RemoteEvent
- [ ] Write "Hello World" in GameManager
- [ ] Test basic server-client communication
