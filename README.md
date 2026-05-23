# 🏙️ Liberty Sands

A single-file, top-down open-world action game inspired by Grand Theft Auto (especially **GTA Advance** on the GBA). 6,500+ lines of vanilla HTML, CSS, and JavaScript packed into one `index.html` file — no build step, no dependencies, no server.

```
  Open index.html in any modern browser.
  Click Play.
  You're in.
```

---

## ✨ Features

- **Hand-designed city** — three islands (Portland, Staunton, Shoreside Vale) connected by bridges, modeled after Liberty City Advance
- **10-mission story arc** with intro/outro narrative beats between missions, ramping environmental mood (clear → overcast → storm → dawn) as the story progresses
- **5 playable characters** with distinct accent colors: Marcus, Rico, Nia, Volk, Echo
- **Real interactive mechanics** beyond shooting: plant bombs (E), hack terminals (E), defend zones, drive chase vehicles, fly planes
- **Stores** — Burger Pit, Pharmacy, Ammu-Nation, Threads — each with their own catalogs
- **Buyable weapons**: pistol, shotgun (spread shot), SMG, rifle, gatling, plus throwable grenades/smoke/molotov cocktails
- **Cheat-only superweapons**: laser cannon, Munroe Bomb (place anywhere, shoot to detonate, screen flashbangs)
- **Military bases** with patrolling soldiers, fighter jets, and an automatic 5-star wanted level the moment you cross the fence
- **Civilian airport** with flyable prop planes and a helicopter
- **Hidden private island** 6,000 units due north — only reachable by plane, $100,000 first-arrival bonus
- **Fake-3D rendering**: oblique-projection extruded buildings with windows, parapet walls, vertical mullions, animated humanoid sprites with arms and walk cycles
- **Procedural sound effects** — every gunshot, explosion, engine rev synthesized via Web Audio API. No audio files anywhere.
- **Procedural textures** — asphalt, concrete, grass, brick all generated at runtime to offscreen canvases
- **Day/night cycle + dynamic weather** — rain particles, lightning + thunder during storms, fog overlay
- **Local multiplayer** — same-browser cross-tab via BroadcastChannel. Lobby codes, host permissions, per-player cheat/mission overrides, broadcast chat
- **Mobile touch controls** — virtual joystick, fire button with auto-aim, action buttons
- **Settings with gameplay assists** — difficulty presets, aim assist, health regen, custom damage multipliers, god mode
- **Full Level Maker** — drop-in custom levels with terrain, NPCs, traffic, cinematics, props
- **In-game chat** — type cheat codes, send messages to the lobby

---

## 🎮 Controls

### Keyboard (Desktop)

| Key | Action |
|---|---|
| **W A S D** | Move |
| **Mouse** | Aim |
| **Left Click** | Fire |
| **Space** | Hold to fire continuously |
| **E** | Interact (enter/exit vehicle, plant charge, hack terminal, open store) |
| **1-7** | Switch weapons (fists, pistol, shotgun, SMG, rifle, gatling, laser) |
| **Q** | Cycle explosive type (grenade → smoke → molotov) |
| **G** | Throw selected explosive |
| **T** or **/** | Focus chat (type cheats or messages) |
| **M** | Open missions list |
| **Tab** or **Esc** | Pause menu (Settings, Multiplayer, Quit) |
| **Mouse wheel** | Zoom in/out |
| **+** / **-** / **0** | Keyboard zoom in/out/reset |

### Mobile (Touch)

Automatic — touch is detected on page load.

| Control | Action |
|---|---|
| **Joystick (left)** | Drag to move |
| **● Fire button (right)** | Hold to fire (auto-aim) |
| **E** | Interact |
| **💣** | Throw explosive |
| **⇄** | Cycle weapon |
| **M** | Missions |
| **💬** | Focus chat |

---

## 💀 Cheat Codes

Press **T** in-game to open chat. Type a code and press Enter.

| Code | Effect |
|---|---|
| `eee^` | Fly mode + opens the inline Developer Panel |
| `iii$` | Infinite money (set to 999,999,999) |
| `uue!` | Spawn & equip the Laser Cannon (cheat-only weapon) |
| `gt*` | Spawn & equip the Gatling Gun |
| `st+` | 10-star wanted level — every branch of the military hunts you |
| `hp%` | Heal to full health |
| `ar#` | Refill armor |
| `bm$` | +$100,000 |
| `cl$` | Zero out money (disables infinite money cheat too) |
| `pl?` | Spawn a plane next to you |
| `ko^` | Kill every enemy on screen |
| `cl)` | Clear wanted level |
| `wp~` | Grant all weapons |
| `nv&` | Toggle day/night |
| `gd(` | Toggle god mode |
| `zn%` | Spawn a Munroe Bomb (shoot to detonate, flashbangs the screen, kills every NPC on the map) |

Type `/help` in chat to list all codes at runtime.

---

## 🎯 Missions

10 connected story missions following Marcus's crew unraveling a conspiracy.

Each mission:
- Has a **gold waypoint pillar** in the world marking where to go
- Auto-swaps the player to the appropriate character (Marcus, Rico, Nia, Volk, or Echo)
- Pays out a **cash reward** scaling as `id × id × 500` ($500 → $50,000 for Mission 10)
- Locked until the previous mission is complete (the Dev Panel cheat lets you replay or skip)
- Triggers a **Story Interlude** overlay between missions linking the narrative

Beat all 10 to unlock the **Level Maker**.

The world's environment shifts as the story progresses:
- Mission 1: midday clear
- Mission 3: fog rolls in
- Mission 5: pre-dawn thunderstorm
- Mission 10: evening clear ("the city sleeps")

---

## 🤝 Multiplayer

**Note:** Multiplayer currently only works between browser tabs on the **same machine** (via the `BroadcastChannel` API). Cross-internet play would need a WebSocket relay server — see [Future Work](#future-work).

### How it works

1. Title screen → **MULTIPLAYER**
2. **Create Lobby** → generates a 6-character code, shows it big
3. Open another browser tab on the same machine, go to the same page
4. **MULTIPLAYER** → **Join with Code** → enter the code
5. Both tabs see each other in the player list
6. **Host clicks ▶ Start** — both tabs auto-enter the world

### Host permissions

The host's lobby panel includes:
- **Master switch**: Allow cheats for non-host players
- **Per-cheat toggles**: individually allow/block each of 16 cheats
- **Allow players to start missions**
- **Per-player overrides**: every connected player has their own cheats / missions checkboxes

Permissions broadcast in real time via the BroadcastChannel.

### What's synced

- Player position, angle, walk animation
- Currently equipped weapon (visible on remote player sprite)
- Chat messages
- Lobby permissions

### What's NOT synced

- Enemies, missions, vehicles, bullets — each player has their own world simulation
- Saved progress

---

## 🛠️ Level Maker

Unlocked after beating all 10 story missions.

The editor has 8 categorized toolbars:

- **World & Environment** — terrain blocks, sculpting brushes, zone painters, day/night/weather, skybox & ambient light
- **Traffic & Spawning** — vehicle spawn points, traffic paths, parked cars, boat/aircraft zones, no-drive zones, pedestrian spawn zones
- **NPC & Combat** — enemy placement with patrol routes, faction assignment, boss editor, wanted-level trigger zones
- **Mission Logic & Flow** — objective node system, branching paths, checkpoints, timer/score conditions
- **Props & Interactives** — searchable prop library (29 items), destructible tagging, decals, billboards, weapon/health pickups, cover designation, explosion radius previews
- **Cinematics & Audio** — cinematic camera paths, cutscene keyframes, intro/outro builder, trigger zones, ambient sound zones, music regions, NPC dialogue, SFX attachment
- **Testing & System** — minimap icons, difficulty scaler, play-from-cursor, AI playtest bots, heat map overlay, performance metrics
- **File / Social** — version history with autosave, rating & tags, thumbnail capture, collaborative editing toggle, export/share code

Levels save to `localStorage` and can be exported as base64 share codes.

---

## 🏗️ Architecture

**One file. No backend. No build step.** The entire game is inline in `index.html`:

```
<!DOCTYPE html>
<html>
  <head><style>/* ~700 lines of CSS */</style></head>
  <body>
    <!-- ~250 lines of HTML — title, game, editor, overlays -->
    <script>/* ~5,500 lines of JavaScript */</script>
  </body>
</html>
```

### Where state lives

- **`Game`** (JS object in memory) — runtime world: player, buildings, enemies, bullets, particles, camera, time, weather. Cleared on every world regen.
- **`Save`** (persisted to `localStorage`) — durable: money, completed missions, character, settings, inventory, environment state.
- **`MP`** (JS object) — multiplayer state: connected players, lobby code, permissions, channel reference.
- **`LE`** (JS object) — level editor: current level, history, selected tool/object.

### Rendering pipeline (60 fps)

Each frame, in order:

1. **Ground layer** — ocean, sidewalks, parks, water bodies, roads, lane dashes, crosswalks, skid marks, lightlights, fire patches, smoke clouds, thrown projectile shadows
2. **Pickup layer** — health/armor pickup discs with pulsing glow
3. **3D depth-sorted pass** — buildings (with extruded walls, windows, roofs, signs), trees, lamp posts, peds, vehicles, enemies, player, remote multiplayer players, Munroe bombs — all sorted by `y` and drawn back-to-front for proper occlusion
4. **Bullets & particles** — trails, explosions, muzzle flash, blood, sparks
5. **Mission markers** — interactive objects (charges, terminals), defend-zone reticle, waypoint pillar
6. **Weather overlay** — rain particles, fog, lightning flash
7. **Vignette + day/night color grading**
8. **Munroe flashbang** (if active)
9. **Minimap** (drawn separately in its own canvas)

### Procedural assets (no files)

- **Textures** — asphalt, concrete, grass baked once at startup to small offscreen canvases, used as repeating canvas patterns
- **Sound effects** — every audio cue generated at runtime via `AudioContext` oscillators + noise buffers (see the `SFX_PATCHES` object in `index.html`)
- **Sprites** — everything drawn from canvas primitives (circles, rectangles, paths). No image files at all.

### Multiplayer wire format

Messages over the `BroadcastChannel('libsands-lobby-' + code)`:

| Type | Payload | Purpose |
|---|---|---|
| `hello` | `{id, name, character}` | First join announcement (no longer echoed — dedup'd) |
| `leave` | `{id}` | Graceful disconnect |
| `pos` | `{id, name, character, x, y, angle, weapon}` | Position update, fired every 100ms |
| `perms` | `{id, perms}` | Host broadcasts updated permissions |
| `start` | `{id}` | Host signals all clients to enter the game |
| `chat` | `{id, name, text}` | Lobby-wide chat message |

---

## 🚀 Running & Deploying

### Locally

Just **double-click `index.html`**. It opens in your default browser. No installation needed.

For a "real app" feel (no browser chrome), use Chrome/Edge in app mode:

```
"C:\Program Files\Google\Chrome\Application\chrome.exe" --app="file:///C:/path/to/index.html"
```

### Publishing online

The file works on any static host. Free options:

- **Netlify** — drag `index.html` onto the dashboard
- **Cloudflare Pages** — Upload assets workflow
- **GitHub Pages** — push to a public repo, enable Pages in Settings
- **itch.io** — zip and upload as "HTML" project type

All of them give you HTTPS and a public URL automatically. None require a `package.json` or build step.

---

## ⚙️ Settings & Accessibility

In the pause menu (Tab/Esc) → **Settings**:

- Master volume
- Mouse sensitivity
- Show minimap / FPS
- **Difficulty preset** (Easy / Normal / Hard) — auto-configures the assists below
- **Your Damage multiplier** (0.5× – 3×)
- **Incoming Damage multiplier** (0.25× – 2×)
- **Aim Assist** — snap to nearest enemy within a 20° cone
- **Health Regen** — auto-regen 3s after taking damage
- **God Mode** — take no damage

---

## 🧪 Tested in

- Chrome / Edge / Firefox (latest)
- Safari (mostly works; some Web Audio quirks)
- Mobile Chrome on Android
- Mobile Safari on iOS

---

## 🚧 Limitations & Known Issues

- **Multiplayer is local-only** — `BroadcastChannel` doesn't traverse the internet. Cross-machine play needs a WebSocket relay.
- **No persistent shared world** — each player runs their own simulation in their own browser. Killing an enemy in your game doesn't affect anyone else's game.
- **Save data is per-domain, per-browser, per-machine** — moving to another device loses progress unless you manually export.
- **localStorage limit ~5MB** — never likely to hit, but worth knowing.
- **Mobile performance** varies — lots of buildings + many enemies can drop frames on older phones.

---

## 🔮 Future Work

If I were to keep extending this:

- **WebSocket relay** (PartyKit, Cloudflare Durable Objects, or a tiny Node `ws` server) for real online multiplayer
- **Synced game state** — bullets, enemies, missions shared across players
- **Cross-device saves** via Firebase or a simple sync API
- **Asset preloading hooks** so users can opt in to real sprite atlases / mp3s without losing the single-file fallback
- **Splitting the codebase** with a bundler (Vite or esbuild) once it crosses ~10,000 lines — purely for human readability

---

## 📜 License

This project was built collaboratively between a human player/designer and Claude (Anthropic). It uses no third-party assets, libraries, or copyrighted material — everything is original code, procedural generation, or text I wrote during this conversation.

You're welcome to use, modify, and share it however you like. A credit is appreciated but not required.

---

## 🏃 Quick start (TL;DR)

```bash
# Don't have git? Just download index.html and double-click it.
git clone https://github.com/your-username/liberty-sands.git
cd liberty-sands
# That's it. Open index.html in any browser.
```

Press **Play**. Press **M**. Start Mission 1.

When you want to cheat: press **T**, type `iii$`, press Enter.

Good luck out there.
