# BRAVE HERO 平台遊戲 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 2D side-scrolling platformer game (Zelda art style) where a player fights monsters, collects loot, trades at villages, and ultimately defeats the Demon King.

**Architecture:** Single HTML file with embedded CSS + JavaScript. Canvas-based rendering with programmatic sprite generation (Zelda-style pixel art). Web Audio API for music/SFX. Side-scrolling world with camera tracking player. Game systems: combat, inventory, shop, experience/leveling.

**Tech Stack:** HTML5 Canvas, Vanilla JavaScript, Web Audio API

---

## File Structure

- Create: `index.html` — The entire game (HTML + CSS + JS in one file)

This is a single-file browser game. All code lives in `index.html`, organized into clearly commented sections.

---

### Task 1: HTML Shell + Canvas + Game Constants

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create the HTML boilerplate with canvas and base CSS**

```html
<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <title>BRAVE HERO</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { background: #1a1a2e; display: flex; justify-content: center; align-items: center; height: 100vh; overflow: hidden; }
    canvas { border: 2px solid #e6d5a8; border-radius: 4px; }
  </style>
</head>
<body>
  <canvas id="game"></canvas>
  <script>
    // === GAME CONSTANTS ===
    const CANVAS_W = 1280, CANVAS_H = 720;
    const GROUND_Y = CANVAS_H - 100;
    const GRAVITY = 0.6, JUMP_FORCE = -14;
    const TILE_SIZE = 64;
    // ... all game config here
  </script>
</body>
</html>
```

- [ ] **Step 2: Define all game configuration constants**

All monster stats, weapon stats, shop items, XP tables, spawn rules as JS objects.

- [ ] **Step 3: Open in browser to verify canvas renders**

Run: Open `index.html` in browser, verify black canvas with border appears.

---

### Task 2: Input System + Game Loop

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add input handler**

Track WASD keys + mouse left click. Store in `keys` object and `mouse` object.

- [ ] **Step 2: Add game loop with delta time**

`requestAnimationFrame` based loop with `update(dt)` and `render(ctx)`.

- [ ] **Step 3: Add game state machine**

States: `playing`, `menu`, `shop`, `gameover`. S key toggles menu.

- [ ] **Step 4: Verify loop runs**

Open browser, check console for frame updates.

---

### Task 3: World Generation + Camera System

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Create world terrain**

Flat ground with grass tiles. World width = large (many screens). Villages placed every 3+ screen widths apart.

- [ ] **Step 2: Implement camera that follows player**

Camera smoothly tracks player X position. Clamp to world bounds.

- [ ] **Step 3: Draw ground and background**

Zelda-style layered background (sky gradient, distant mountains, grass).

- [ ] **Step 4: Verify scrolling works**

Open browser, use A/D to move, camera should follow.

---

### Task 4: Player Character

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Draw player sprite (Zelda-style adventurer)**

Programmatic pixel art: green tunic, longer arms, brown boots, adventurer hat. Walking animation (4 frames), idle, attack swing animation.

- [ ] **Step 2: Implement player movement**

W=jump (with gravity), A=left, D=right. Player snaps to ground. Walking animation plays on move.

- [ ] **Step 3: Implement player attack**

Left click = swing fist/weapon. Animation shows arm extending. Attack hitbox in front of player.

- [ ] **Step 4: Implement player stats**

HP (5 hearts), money (100), XP (0), inventory array, equipped weapon.

- [ ] **Step 5: Verify player moves and attacks**

Open browser, move with WASD, attack with click. Character should animate.

---

### Task 5: Monster System

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Draw monster sprites (4 tiers)**

Red, Blue, Black, Gold monsters. Each has idle, walk, attack animations. Distinct color palettes. Some hold weapons.

- [ ] **Step 2: Implement monster AI**

Monsters walk toward player when in range. Attack when close. Patrol when player is far.

- [ ] **Step 3: Implement monster spawning rules**

Start 1-3 red monsters. More spawn as kill count rises (max 10). Higher tiers appear based on player HP threshold (player HP > 2× monster attack). Distance: half screen from player on spawn.

- [ ] **Step 4: Implement monster attack animation**

Monsters swing fist or weapon with visible animation.

- [ ] **Step 5: Verify monsters spawn and move**

Open browser, monsters should appear and walk toward player.

---

### Task 6: Combat System

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Implement hit detection**

Player attack hitbox vs monster hitbox. Monster attack hitbox vs player hitbox.

- [ ] **Step 2: Implement damage calculation**

Player damage = weapon damage range (random). Monster damage = hearts based on tier. Weapon durability decreases on hit.

- [ ] **Step 3: Implement knockback**

Hit monster flies backward. Knockback distance proportional to damage.

- [ ] **Step 4: Implement death**

Monster death: drop loot, add XP. Player death: game over screen.

- [ ] **Step 5: Verify combat works**

Fight a red monster, verify HP decreases, monster takes damage, knockback occurs, loot drops.

---

### Task 7: Loot + Inventory + Weapon System

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Implement loot drops**

Monster teeth (always), heart (1/5 chance). Weapon drops based on monster tier and probability table.

- [ ] **Step 2: Implement inventory**

Array of items. Menu (S key) shows inventory: items, weapons, money, XP.

- [ ] **Step 3: Implement weapon switching**

Menu shows owned weapons. Click to equip. Show durability. Auto-switch to fist when weapon breaks.

- [ ] **Step 4: Implement weapon visuals**

Each sword type has matching color. Traveler=blue-green, Soldier=silver, Royal=gold. Drawn in player's hand.

- [ ] **Step 5: Verify loot and weapons**

Kill monsters, check drops appear, pick up weapon, switch via menu.

---

### Task 8: Experience + Leveling

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Implement XP gain on kill**

Red=10, Blue=15, Black/Gold=20 XP.

- [ ] **Step 2: Implement level up**

Every 100 XP: max hearts +1, full heal. Visual/audio feedback on level up.

- [ ] **Step 3: Verify leveling**

Kill enough reds (10), verify level up, heart increase, full heal.

---

### Task 9: Village + Shop System

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Draw village assets**

Zelda-style buildings, NPCs, shop sign. All grounded on floor. Village boundaries clearly marked.

- [ ] **Step 2: Implement village zones**

No monsters spawn in village area. Player can freely enter/exit.

- [ ] **Step 3: Implement village music**

Web Audio API: peaceful countryside melody. Plays when in village, stops when leaving.

- [ ] **Step 4: Implement shop UI**

Beautiful shop interface. Each item (Apple, Roast Meat, Porridge, Fish) has a generated icon/image. Buy with money. Sell teeth/hearts.

- [ ] **Step 5: Implement item consumption**

Buy food → goes to inventory. Use from menu → heal specified amount.

- [ ] **Step 6: Verify village and shop**

Enter village, music plays. Open shop, buy apple, use it, verify heal. Sell teeth. Leave village, music stops, monsters appear.

---

### Task 10: HUD + UI Polish

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Draw HUD**

Hearts display (top-left), money (top-right), XP bar, equipped weapon + durability, minimap hint.

- [ ] **Step 2: Draw menu screen**

S key opens: inventory grid, weapon list, player stats. Zelda-style UI frame.

- [ ] **Step 3: Add game over screen**

Death → "Game Over" with restart option.

- [ ] **Step 4: Add start screen**

Title "BRAVE HERO" with "Press any key to start".

- [ ] **Step 5: Verify all UI elements**

Check HUD updates in real-time, menu works, game over triggers correctly.

---

### Task 11: Audio + Visual Polish

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add sound effects**

Attack swing, hit, monster death, item pickup, level up, shop buy/sell. All via Web Audio API oscillators.

- [ ] **Step 2: Add combat music**

Energetic background music for wilderness areas.

- [ ] **Step 3: Add particle effects**

Hit sparks, death poof, level up glow, loot sparkle.

- [ ] **Step 4: Polish animations**

Smooth transitions, screen shake on big hits, damage numbers floating up.

- [ ] **Step 5: Final playtest**

Play through: start → fight monsters → level up → visit village → buy items → fight harder monsters. Verify all systems work together.

---

### Task 12: Final Integration + Boss Teaser

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Balance pass**

Adjust spawn rates, damage values, item prices for fun gameplay loop.

- [ ] **Step 2: Add difficulty progression**

Ensure monster tier escalation feels smooth. Gold monsters should feel like a real challenge.

- [ ] **Step 3: Commit final version**

```bash
git add index.html
git commit -m "feat: complete BRAVE HERO platformer game v1.0"
```
