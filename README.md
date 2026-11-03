# GrowBlox Auto Plant (Roblox Studio)

Starter project for a game you own/control. This is not an executor script and is not intended for use in someone else's experience.

## Files
- `AutoPlantServer.server.lua` — server-side validation, seed inventory check, plant placement, and RemoteEvent/RemoteFunction setup.
- `AutoPlantGUI.client.lua` — draggable mobile-friendly GUI with seed cycling, delay, Start, Stop, status, and count.

## Roblox Studio setup

1. In `ReplicatedStorage`, create a Folder named `SeedModels`.
2. Put one Model per seed inside `SeedModels`. Example names: `Carrot`, `Tomato`, `Corn`.
   - Each Model should have a sensible pivot and visible parts.
3. In `Workspace`, create a Folder named `PlantSpots`.
4. Put one BasePart per planting location inside `PlantSpots`. Name them uniquely (`Spot1`, `Spot2`, ...).
5. For each spot, add a Number Attribute named `OwnerUserId` and set it to the owning player's Roblox UserId.
6. Add `AutoPlantServer.server.lua` as a Script in `ServerScriptService`.
7. Add `AutoPlantGUI.client.lua` as a LocalScript in `StarterPlayer > StarterPlayerScripts`.
8. Ensure the player has seed inventory attributes, for example `Seed_Carrot = 10`. Set these from your own server-side inventory system.

## Studio-only inventory test example

Put this temporary Script in `ServerScriptService` while testing, and remove it when connecting your real inventory system:

```lua
game.Players.PlayerAdded:Connect(function(player)
    player:SetAttribute("Seed_Carrot", 20)
    player:SetAttribute("Seed_Tomato", 20)
    player:SetAttribute("Seed_Corn", 20)
end)
```

The attribute names must match `Seed_` plus the exact Model name in `SeedModels`.

## Important notes
- The server creates `ReplicatedStorage/AutoPlantRemotes` and its RemoteEvent/RemoteFunction automatically.
- The server checks that the spot belongs to the requesting player, is empty, and that the player has the selected seed.
- A spot is marked `Planted = true` after a successful plant. Your game needs its own harvest/reset logic to set it back to false.
- This starter example does not include saving inventory, crop growth stages, harvesting, plot assignment, or DataStore persistence.
- Test in a private Studio session before publishing.
