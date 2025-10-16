# VR Duel Study Project
## 🏁 Summary
This project demonstrates:
- A functional Photon Fusion 2 network loop
- A hybrid VR interaction system
- Structured, scalable multiplayer architecture
- Production-ready understanding of scene flow, authority, and state sync
- The remaining bugs are minor synchronization issues that would take a few focused hours to resolve.

## 📋 Usage Instructions
1. Clone the repository.
2. Open either version folder:
	- VR Runner
	- Flat Runner (non-vr) [for testing without a headset only]
3. Run the EXE
4. You will be asked to enter a username
	- if the keyboard fails to appear just press continue and a random
	one will be supplied 
5. Press play to automatically be placed in a lobby w/ other players
6. Once the project boots up, feel free to take a look around the room.
5. To challenge a player to a duel:
	VR:
	- Smack them with your large red hand to send them a duel request
	Flat:
	- Left click to raycast them and send a duel request
6. Once accepted both players will be taken into a private 1v1 room
7. The duel is first player to 3 wins
	- Score may desync on one of the clients
	this is only a visual bug and logic still functions
8. Once the duel is over, player stats will be recorded locally
and both players will bereturned back to the lobby

# Project Details
## ⚙️ Implemented Systems

### 🧍 Player Interaction
- Hybrid locomotion using AutoHand + Gorilla Tag–style physics.
- Joystick movement, climbing, ledge hangs, monkey bars, push-off locomotion.
- Mirror and cosmetic preview system (with cape, bow tie, and hat placeholders).
- Fully functional wardrobe menu for future outfit selection.

### 🌐 Networking (Fusion 2 Shared Mode)
- Deterministic Runner bootstrap with scene flow: Menu → Lobby → Duel.
- Duel broker RPC system
- Player “slaps” another to send a duel request.
- Target receives popup UI with Accept/Decline.
- Shared authority room handoff with synchronized roomName.
- ScoreBroker
- Tracks per-round scores, resets, and win conditions.
- Handles health resets, round transitions, and game shutdown.
- Networked Player Data (INetworkedPlayerData, PlayerDuelData)
- Syncs name, health, and player flags across peers.

### 💥 Combat (WIP)
- Prototype weapons: sword, spear, pistol, throwing discs, dagger, and grenade.
- All networked objects are pickup-ready using AutoHand’s interaction layer.
- Damage logic functional; hit events trigger RPCs and update score.

### 🧠 UI / UX
- Dynamic Score UI showing:
- Local and remote player names
- Per-round score and win/lose status
- Health bar updates with smooth fill interpolation
- Lobby vote panel (stubbed for now).
- Networked mirror camera for third-person reflection.

## Would Be Next Steps
- Replace local event-based UI hooks with full network-replicated hydration.
- Finalize weapon network ownership + damage authority.
- Expand arenas and voting system.
- Add Spectator Mode for extra players waiting in lobby.
- Implement Supabase integration for stats persistence.

## 🚧 Known Issues
### UI Sync
Remote player's UI sometimes doesn’t refresh (late join / host migration).
### Round Reset
Only one player teleports after a round ends.
### Scene Loop
Occasionally the editor instance re-loads the duel scene twice.
### Weapon Netcode
Weapons somtimes not assigned dynamic network ownership on pickup.

# Project Structure

### Scenes
Assets/_Workspace_/Geo/Scenes/<br />
 ├── MainMenu<br />
 ├── Duel_Medieval_Detailed<br />
 
### Network Script Architecture overview
Bootstrap.cs<br />
 ├─ Manages persistent NetworkRunner<br />
 ├─ Handles scene transition + shutdown sequencing<br />
 ├─ Keeps global state (AutoStart, DuelRoomName, etc.)<br />

DuelBroker.cs<br />
 ├─ Mediates player challenge requests<br />
 ├─ Sends duel offers and confirmations via RPCs<br />

ScoreBroker.cs<br />
 ├─ Tracks duel state, round reset, win condition<br />
 ├─ Synchronizes player scores<br />
 ├─ Dispatches round reset RPCs<br />

PlayerDuelData.cs<br />
 ├─ Networked player state (health, name)<br />
 ├─ Handles damage, respawn, and visual feedback<br />

ScoreUI.cs<br />
 ├─ Reflects ScoreBroker network state<br />
 ├─ Displays names, health, and win/lose feedback<br />

## 🗣️ Developer Note / Final Thoughts
“I treated this as if it were a vertical slice of a small commercial VR title, getting the systems right mattered more to me than polishing every feature. Open to walk through how each part of the architecture works and where I’d take it next.”
- Gianni Rivero
