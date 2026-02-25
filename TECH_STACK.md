# Tech Stack - Mechanical Restaurant Horror

## Roblox Lua Modules Needed

### Core Systems
1. **StateMachine** — Handle game states (Lobby → Day → Night → Day...)
2. **EventManager** — Centralized RemoteEvent handling
3. **DataManager** — Player data (if using DataStore)
4. **TickManager** — Day/night timing

### Gameplay Systems
5. **CustomerAI** — Customer behavior, ordering, leaving
6. **CookingSystem** — Timers, recipes, food items
7. **InventorySystem** — Player-held items
8. **CombatManager** — Kill button, weapons
9. **AIManager** — Mechanical animal pathfinding

### UI Systems
10. **UIController** — GUI state management
11. **NotificationSystem** — Popups, alerts

---

## Roblox Services Used

| Service | Use Case |
|---------|----------|
| `TweenService` | UI animations, door movements |
| `Debris` | Cleaning up objects |
| `PathfindingService` | Mechanical animal movement |
| `PhysicsService` | Collision groups |
| `ReplicatedStorage` | Shared data & RemoteEvents |
| `ServerStorage` | Private assets |
| `DataStoreService` | Persistent player data (optional) |
| `MarketplaceService` | Game passes / developer products |
| `SoundService` | Audio management |
| `Lighting` | Day/night atmosphere |

---

## Key Technical Decisions

### Multiplayer Sync
- Use `RemoteEvents` for server-client communication
- Server authoritative (don't trust client for critical game state)
- Use `Leaderstats` for visible player stats

### Day/Night Implementation
- Change `Lighting` properties (Ambient, Brightness, TimeOfDay)
- Tween settings for smooth transitions
- Separate timer from game clock

### Customer Spawning
- Object pooling for performance
- Random spawn points in dining area
- Queue system if max customers reached

### AI Pathfinding
- `PathfindingService` for mechanical animals
- Simple "move to nearest player" behavior
- Check line of sight before spawning

### Performance Considerations
- Limit max NPCs (e.g., 8 customers + 4 animals)
- Use `Debris:AddItem()` for cleanup
- LOD for distant objects
- Limit particle effects

---

## Sample Code Structure

### GameManager (Main Loop)
```lua
local GameState = {
    LOBBY = "Lobby",
    DAY = "Day", 
    NIGHT = "Night",
    GAME_OVER = "GameOver"
}

local currentState = GameState.LOBBY
local currentDay = 1

local function cycleGame()
    while true do
        if currentState == GameState.LOBBY then
            waitForPlayers()
            startGame()
        elseif currentState == GameState.DAY then
            runDayPhase()
        elseif currentState == GameState.NIGHT then
            runNightPhase()
        end
    end
end
```

### RemoteEvent Pattern
```lua
-- Server
local killEvent = ReplicatedStorage.KillCustomer
killEvent.OnServerEvent:Connect(function(player, customer)
    -- Validate, apply penalty, notify clients
end)

-- Client
local killButton = ...
killButton.MouseButton1Click:Connect(function()
    killEvent:FireServer(customer)
end)
```

---

## Useful Roblox Lua Patterns

### Module Scripts
```lua
-- MyModule.lua
local MyModule = {}
MyModule.__index = MyModule

function MyModule.new()
    local self = setmetatable({}, MyModule)
    return self
end

return MyModule
```

### Events with Delay
```lua
task.delay(5, function()
    -- Do something after 5 seconds
end)

task.spawn(function()
    -- Run concurrently
end)
```

---

## Debugging Tips

1. Use `print()` for quick debugging
2. Check Output panel in Studio
3. Use `warn()` for non-critical issues
4. Test in both Studio and actual game
5. Use `debug.profilebegin()` for performance

---

## External Resources

- [Roblox Developer Hub](https://developer.roblox.com/)
- [Lua Documentation](https://www.lua.org/manual/5.1/)
- [Roblox Wiki](https://roblox.fandom.com/wiki/Roblox_Wiki)
