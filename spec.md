# Dicero — Game Design Specification

## Overview

**Dicero** is a single-player roguelike deckbuilder where poker is replaced by Yahtzee-style dice rolling. Inspired by Balatro's structure, players roll dice to form scoring combinations, collect **Charms** (passive modifiers), use **Blessings** to level up scoring categories, and apply **Enchantments** to modify individual dice — all while progressing through five increasingly difficult **Trials**, each culminating in a boss encounter with a unique modifier.

**Theme:** Mystical / arcane. The player is a wandering sorcerer rolling ancient dice in enchanted trials. Enemies are magical creatures and corrupted spirits. Charms are artifacts of power. The dice themselves are relics of a forgotten age.

---

## Core Mechanics

### Dice Rolling

- The player rolls **5 dice** (standard six-sided, faces 1–6).
- After each roll, the player may **keep** any number of dice and **reroll** the rest.
- The player gets **3 rerolls** per round (initial roll + 3 rerolls = 4 total roll opportunities).
- After the final reroll (or when the player chooses to stop), the player **scores** the dice against a chosen scoring category.

### Scoring Formula

**Score = Base Score × Multiplier**

- **Base Score** = sum of the scored dice faces, plus any bonus chips from the scoring category's level and from Charms.
- **Multiplier** = the category's base mult, plus any mult bonuses from Charms, Enchantments, and category levels.

This mirrors Balatro's `Chips × Mult` formula. The two scaling axes (chips and mult) create the same exponential growth potential that makes Balatro's builds satisfying.

### Scoring Categories

These are the Yahtzee-style hands the player can form. Each category has a **base chip value** and a **base mult value** that increase when leveled up with Blessings.

| Category | Description | Base Chips | Base Mult |
|---|---|---|---|
| **Ones through Sixes** | Sum of all dice showing that number | 5 | 1 |
| **Three of a Kind** | At least 3 dice showing the same value; score = sum of all dice | 30 | 3 |
| **Four of a Kind** | At least 4 dice showing the same value; score = sum of all dice | 60 | 5 |
| **Full House** | 3 of one value + 2 of another | 40 | 4 |
| **Small Straight** | 4 sequential dice (e.g., 1-2-3-4 or 3-4-5-6) | 45 | 4 |
| **Large Straight** | 5 sequential dice (1-2-3-4-5 or 2-3-4-5-6) | 80 | 7 |
| **Yahtzee** | All 5 dice showing the same value | 100 | 10 |
| **Chance** | Any combination; score = sum of all dice | 15 | 2 |

**Note:** Unlike traditional Yahtzee, categories are **not** consumed after use. The player can score the same category multiple times across rounds. This is essential for build-crafting — if your build is centered around Full Houses, you need to be able to play them repeatedly.

### Hands and Discards (per Enemy Encounter)

- The player has a limited number of **hands** (attempts to score) per encounter, starting at **4 hands**.
- The player has a limited number of **discards** — situations where they can reroll all 5 dice without it counting as a hand, starting at **3 discards**.
- A discard lets you throw away a bad roll entirely and start fresh, at the cost of one discard use.
- If the player's cumulative score across all hands meets or exceeds the enemy's **target score**, the encounter is won. If they run out of hands, the run ends.

---

## Progression: The Five Trials

Each run consists of **5 Trials**. Each Trial contains **5 enemy encounters** and **1 boss encounter** (6 total per Trial). Target scores increase with each encounter and each Trial.

After every encounter (except the boss), the player visits the **Shop**.

### Score Scaling

Base target scores increase per Trial. Within each Trial, the 5 enemies scale from 1× to ~2.5× the Trial's base, and the boss is 3× the Trial's base.

| Trial | Base Target | Enemy Range | Boss Target |
|---|---|---|---|
| Trial 1: The Ember Sanctum | 300 | 300 – 750 | 900 |
| Trial 2: The Hollow Depths | 1,500 | 1,500 – 3,750 | 4,500 |
| Trial 3: The Shattered Spire | 8,000 | 8,000 – 20,000 | 24,000 |
| Trial 4: The Obsidian Rift | 40,000 | 40,000 – 100,000 | 120,000 |
| Trial 5: The Astral Throne | 200,000 | 200,000 – 500,000 | 600,000 |

*(Numbers are approximate. Tuning required through playtesting.)*

---

## Enemies

Each enemy within a Trial is a named creature with flavor text and a **minor passive effect** that adds variety without being as disruptive as a boss modifier. Enemies are drawn from a pool for each Trial, so runs feel different each time.

### Trial 1: The Ember Sanctum
*A crumbling temple lit by dying embers. The ancient guardians still stir.*

| Enemy | Passive Effect |
|---|---|
| **Cinder Imp** | No effect. (Introductory encounter.) |
| **Ash Wraith** | Your first reroll each hand scores 0 bonus chips from Charms. |
| **Ember Golem** | Ones count as 0 for chip calculation (but still count for combinations). |
| **Flame Keeper** | Target score increases by 50 for each hand you use. |
| **Molten Sentinel** | Dice showing 6 are "scorched" — they can't be kept between rerolls. |
| **BOSS: Pyraxxus, the Undying Flame** | *Boss modifier: All dice showing a randomly selected number (chosen at start) are debuffed — they contribute 0 chips and don't trigger Charm effects.* |

### Trial 2: The Hollow Depths
*Beneath the earth, in fungal caverns and flooded crypts, forgotten things lurk.*

| Enemy | Passive Effect |
|---|---|
| **Spore Crawler** | After your first reroll, one random kept die is rerolled. |
| **Blind Burrower** | Two of your dice are "hidden" (face-down) until scored. You don't see their values during rerolls. |
| **Fungal Shaman** | Chance category is disabled. |
| **Drowned Revenant** | You start each hand with only 2 rerolls instead of 3. |
| **Crystal Lurker** | Dice can only show values 1–5 (sixes are rerolled automatically). |
| **BOSS: Gloomjaw, the Depth Devourer** | *Boss modifier: After each hand, the lowest-scoring category you've used this encounter is "devoured" — it becomes unavailable for the rest of the encounter.* |

### Trial 3: The Shattered Spire
*A broken tower piercing the clouds. Wind and lightning rage through fractured halls.*

| Enemy | Passive Effect |
|---|---|
| **Gale Phantom** | After each reroll, one of your kept dice is randomly swapped with a rerolled die. |
| **Storm Elemental** | Even-numbered dice give half chips (rounded down). |
| **Rune Breaker** | Your highest-level scoring category has its level reduced by 1 for this encounter. |
| **Skyborne Sentinel** | You must score with at least 3 dice or the hand scores 0. |
| **Shardcaster** | One random Charm is disabled for this encounter. |
| **BOSS: Voltaryx, the Spire's Crown** | *Boss modifier: You cannot score the same category twice in a row. Must alternate.* |

### Trial 4: The Obsidian Rift
*A crack in reality where dark glass and void energy twist the laws of chance.*

| Enemy | Passive Effect |
|---|---|
| **Void Flickerer** | At the start of each hand, one die is "phased" — it shows a random value that changes on every reroll and can't be kept. |
| **Glass Stalker** | Scoring a Three of a Kind or lower category deals 10% of your scored amount back as "chip damage" — it's subtracted from your cumulative score. |
| **Rift Weaver** | All dice values are inverted (1↔6, 2↔5, 3↔4) for chip calculation but not for combination purposes. |
| **Obsidian Warden** | You have 1 fewer hand this encounter. |
| **Null Prophet** | Mult bonuses from Charms are halved (rounded down). |
| **BOSS: Nihilex, the Rift Warden** | *Boss modifier: Two numbers (randomly chosen) cannot be scored. Dice showing those numbers contribute 0 chips and don't count toward combinations.* |

### Trial 5: The Astral Throne
*Beyond the mortal plane. The stars themselves are your opponents.*

| Enemy | Passive Effect |
|---|---|
| **Stellar Wisp** | Your rerolls cost $1 each (from your gold). |
| **Constellation Beast** | Only categories using all 5 dice (Yahtzee, Large Straight, Chance with all 5) give full mult. Others give half mult. |
| **Astral Arbiter** | You must beat a minimum score of 20,000 on each individual hand, or it counts as 0. |
| **Celestial Mimic** | Copies the passive effect of a random enemy from a previous Trial. |
| **Fate Spinner** | After you choose dice to keep, there's a 25% chance each kept die rerolls anyway. |
| **BOSS: Aeonax, the Final Arbiter** | *Boss modifier: Three numbers are banned (randomly chosen). Additionally, you have 1 fewer hand and 1 fewer discard. The ultimate test.* |

---

## Charms

Charms are the core build-defining element — equivalent to Balatro's Jokers. The player collects Charms from the Shop and holds them in **Charm Slots** (starting with 5 slots, expandable). Charms are persistent across the entire run until sold or destroyed.

### Charm Rarities

| Rarity | Shop Appearance Rate | Typical Power Level |
|---|---|---|
| **Common** | 70% | Small, reliable bonuses |
| **Uncommon** | 25% | Conditional or scaling bonuses |
| **Rare** | 5% | Powerful build-defining effects |
| **Legendary** | Special (from Spectral Enchantments only) | Game-warping effects |

### Charm Activation Types

Mirroring Balatro's joker activation system:

| Activation Type | When It Triggers | Example |
|---|---|---|
| **On Roll** | When dice are rolled (including rerolls) | "Each time you roll, gain +1 chip for every die showing 4 or higher." |
| **On Keep** | When the player locks in dice to keep | "Each kept die adds +1 mult." |
| **On Score** | When individual dice contribute to the final score | "Each scored die showing 6 gives +4 mult." (Triggers per die, benefits from retriggers.) |
| **On Reroll** | When the player rerolls dice | "Every reroll gives +2 mult if you rerolled 3 or more dice." |
| **On Category** | When a specific category is scored | "Scoring a Full House gives +20 chips." |
| **Independent** | After all dice are scored, flat bonus | "+4 mult." / "+30 chips." |
| **Scaling** | Permanent stat gains over the course of the run | "Gains +3 chips every time you score a Straight." |
| **Economy** | Provides money or shop advantages | "Earn $3 at end of each encounter." |
| **Passive** | Always-on effects that change game rules | "Straights can wrap around (e.g., 5-6-1-2-3 counts)." |

### Example Charms (30 examples across rarities)

#### Common Charms
1. **Lucky Penny** — +3 chips. (Independent)
2. **Iron Die** — +2 mult. (Independent)
3. **Snake Eyes** — +10 chips whenever you roll double 1s. (On Roll)
4. **Steady Hand** — +1 mult for each die you keep on your first reroll. (On Keep)
5. **Copper Ring** — Earn +$1 after each encounter. (Economy)
6. **Warm Ember** — Dice showing 1 give +3 chips when scored. (On Score)
7. **Loaded Bones** — +5 chips when you score Chance. (On Category)
8. **Gambler's Grin** — +1 mult per reroll used in a hand. (On Reroll)
9. **Tallow Candle** — +8 chips if you score using exactly 2 dice. (On Score)
10. **Field Mouse** — If you score less than 100 on a hand, gain $2. (Economy)

#### Uncommon Charms
11. **Obsidian Shard** — Each die showing 6 gives ×1.5 mult when scored. (On Score)
12. **Fortune's Wheel** — Gains +2 chips permanently every time you reroll all 5 dice. (Scaling)
13. **Echoing Die** — The highest-value scored die triggers twice. (On Score / Retrigger)
14. **Bone Abacus** — Gains +1 mult permanently every time you score Four of a Kind. (Scaling)
15. **Third Eye** — You can see the next reroll's results before choosing to keep. (Passive)
16. **Snake Charmer** — Small Straights give +15 chips. (On Category)
17. **Hexed Coin** — Earn +$4 per encounter, but lose $2 whenever you use a discard. (Economy)
18. **Stone Mask** — If all 5 dice show different values, +6 mult. (On Score)
19. **Blood Pact** — +8 mult, but you have 1 fewer hand per encounter. (Independent / Drawback)
20. **Mimic Charm** — Copies the effect of your leftmost Common Charm. (Passive)

#### Rare Charms
21. **Chrono Die** — Gain +1 reroll per encounter. (Passive)
22. **The Ouroboros** — Gains +5 chips and +1 mult every time you fail to beat an enemy, persists across encounters. (Scaling)
23. **Prismatic Lens** — All Charm effects that give flat chips also give that amount as mult (at half value). (Passive)
24. **Fate Bender** — Once per encounter, you can set one die to any face value. (Passive / Active)
25. **Golden Bones** — ×2 mult if you have $20 or more. (Independent / Conditional)
26. **Chaos Orb** — On each roll, one random die becomes a "wild" — it counts as any value for combination purposes. (On Roll)
27. **Void Siphon** — When an enemy's passive effect would reduce your score, gain +3 mult instead. (Passive / Reactive)

#### Legendary Charms
28. **The First Die** — All dice gain +1 to their face value (a die showing 6 counts as 7). Breaks the normal 1–6 range. (Passive)
29. **Paradox Engine** — Whenever you score, there is a 20% chance your mult is squared instead of multiplied. (On Score)
30. **Eternity's Gambit** — At the start of each encounter, choose any scoring category — it scores at ×3 mult for the entire encounter. (Passive / Active)

---

## Enchantments

Enchantments are consumable items that **modify individual dice** — equivalent to Balatro's Tarot cards. The player can hold up to **2 Enchantments** at a time (expandable). Each Enchantment is single-use and permanently alters a targeted die for the rest of the run.

### Dice Modifications (applied via Enchantments)

| Modification | Effect | Visual |
|---|---|---|
| **Weighted** | This die always rolls 4, 5, or 6. | Glowing gold edges |
| **Lucky** | This die has a 1 in 4 chance to trigger twice when scored. | Green shimmer |
| **Steel** | +4 mult when this die is kept but NOT part of the scoring combination. | Metallic sheen |
| **Gilded** | +10 chips when this die is scored. | Gold-plated face |
| **Void** | This die contributes ×1.5 mult when scored, but 0 chips. | Dark purple aura |
| **Wild** | This die counts as any value for combination purposes (player's choice). | Rainbow glow |
| **Cursed** | +8 mult when scored, but -1 hand for the encounter if this die shows a 1. | Red cracks |
| **Mirrored** | When scored, this die's value is also added as mult. | Reflective surface |

### Enchantment Cards (found in shop, from encounters, or from special events)

Examples:
- **Rune of Iron** — Apply the Steel modification to a die.
- **Goldweave** — Apply the Gilded modification to a die.
- **Shadow Ink** — Apply the Void modification to a die.
- **Chaos Rune** — Apply the Wild modification to a die.
- **Fate's Favor** — Apply the Lucky modification to a die.
- **Dark Bargain** — Apply the Cursed modification to a die.
- **Artisan's Touch** — Remove a modification from a die.
- **Transmute** — Change one die modification into a random different one.
- **Shatter** — Destroy a die modification. Gain $5.

A single die can only hold **one modification** at a time. Applying a new one replaces the old.

---

## Blessings

Blessings are consumable items that **level up scoring categories** — equivalent to Balatro's Planet cards. The player can hold up to **2 Blessings** at a time (expandable).

Each use of a Blessing permanently increases the base chips and base mult of the targeted category.

| Blessing | Target Category | Chips per Level | Mult per Level |
|---|---|---|---|
| **Blessing of Embers** | Ones | +5 | +1 |
| **Blessing of Tides** | Twos | +5 | +1 |
| **Blessing of Stone** | Threes | +5 | +1 |
| **Blessing of Wind** | Fours | +5 | +1 |
| **Blessing of Stars** | Fives | +5 | +1 |
| **Blessing of Shadow** | Sixes | +5 | +1 |
| **Blessing of Harmony** | Full House | +15 | +2 |
| **Blessing of Triplicity** | Three of a Kind | +10 | +1 |
| **Blessing of Dominion** | Four of a Kind | +15 | +2 |
| **Blessing of the Path** | Small Straight | +15 | +2 |
| **Blessing of the Journey** | Large Straight | +20 | +3 |
| **Blessing of Perfection** | Yahtzee | +25 | +4 |
| **Blessing of Fortune** | Chance | +10 | +1 |

---

## Economy & Shop

### Currency

The player earns **Gold ($)** after each encounter:
- Base payout: $3 for regular enemies, $5 for bosses
- Bonus: +$1 for each unused hand
- Bonus: +$1 for each unused discard
- Interest: +$1 for every $5 held (max $5 interest, i.e., caps at $25 held)

### The Shop

After each non-boss encounter, the player visits the Shop. The shop offers:

| Slot | Contents |
|---|---|
| **2 Charm slots** | Random Charms for purchase (rerollable for $1) |
| **1 Blessing slot** | Random Blessing for purchase |
| **1 Enchantment slot** | Random Enchantment for purchase |
| **1 Consumable/Special slot** | Rotating specials (see below) |

#### Shop Prices (base)
- Common Charm: $4–6
- Uncommon Charm: $7–10
- Rare Charm: $12–16
- Blessing: $3–5
- Enchantment: $4–7
- Reroll shop: $1 (increases by $1 each reroll per visit)

#### Selling
- The player can sell Charms from their Charm slots at any time in the shop for half their purchase price.
- Selling is strategic — sometimes you need to dump a Charm to afford a better one or free up a slot.

### Special Shop Items (Consumable Slot)

These are one-off purchases that provide immediate or encounter-long effects:

- **Extra Hand Scroll** — +1 hand for the next encounter. ($3)
- **Extra Reroll Scroll** — +1 reroll for the next encounter. ($3)
- **Dice Polish** — One random die is rerolled to a 6 at the start of your next hand. ($4)
- **Merchant's Map** — Next shop has 1 extra Charm slot. ($4)
- **Spectral Shard** — Reveals a Legendary Charm in the next shop (still must purchase). ($8)
- **Charm Slot Expansion** — Permanently gain +1 Charm slot. ($10, appears rarely)

---

## Run Structure — Full Flow

```
START RUN
│
├─ Choose Starting Bonus (pick 1 of 3 random Charms)
│
├─ TRIAL 1: The Ember Sanctum
│   ├─ Enemy 1 → Shop
│   ├─ Enemy 2 → Shop
│   ├─ Enemy 3 → Shop
│   ├─ Enemy 4 → Shop
│   ├─ Enemy 5 → Shop
│   └─ BOSS: Pyraxxus → Reward (rare Charm or Blessing choice)
│
├─ TRIAL 2: The Hollow Depths
│   ├─ Enemy 1 → Shop
│   ├─ ... (same structure)
│   └─ BOSS: Gloomjaw → Reward
│
├─ TRIAL 3: The Shattered Spire
│   └─ ... (same structure)
│
├─ TRIAL 4: The Obsidian Rift
│   └─ ... (same structure)
│
├─ TRIAL 5: The Astral Throne
│   ├─ Enemy 1 → Shop
│   ├─ ...
│   └─ FINAL BOSS: Aeonax → WIN
│
└─ END RUN (Victory!)
    └─ Unlock new starting bonuses, Charms, etc.
```

### Between Trials

After defeating a Trial's boss, before entering the next Trial, the player receives a **Trial Reward**:
- Choice of 1 of 3: a Rare Charm, a high-level Blessing, or a large gold bonus ($15).
- This is the primary way to get Rare Charms outside of lucky shop rolls.

---

## Unlockables & Meta-Progression

Completing runs and achieving milestones unlocks new content for future runs:

### Unlockable Charms
- Defeating each boss for the first time unlocks a new Charm in the pool.
- Winning a full run unlocks Legendary Charms in the Spectral Shard pool.

### Starting Dice Sets
Instead of Balatro's deck selection, the player can unlock **Dice Sets** — starting configurations that change the rules:

| Dice Set | Effect |
|---|---|
| **Standard Bones** | Default. No modifier. |
| **Loaded Set** | All dice start Weighted, but you begin with only 4 Charm slots. |
| **Gambler's Set** | Start with $15 extra gold but 1 fewer hand per encounter. |
| **Chaos Set** | All dice start Wild, but Blessings cost double. |
| **Minimalist Set** | Start with only 3 dice but +2 rerolls. Unlocks a 4th die from a special shop item. |
| **Cursed Set** | Start with +3 mult on all categories, but every enemy has an additional random passive. |
| **Gilded Set** | All dice start Gilded, but shops only offer 1 Charm slot instead of 2. |

---

## UI / UX Notes

### Main Play Screen
- **Center:** The 5 dice, large and prominent. Kept dice slide up, reroll dice bounce in place.
- **Left sidebar:** Charm slots (showing all active Charms with hover-over descriptions).
- **Right sidebar:** Available scoring categories with current chip/mult values and level indicators.
- **Top:** Current encounter info (enemy name, target score, current cumulative score, hands/discards remaining).
- **Bottom:** Action buttons (Roll, Keep, Score, Discard).

### Visual Feedback
- Scoring should have a **dramatic calculation sequence** (like Balatro's chips × mult animation) where you see each die's contribution, then Charm effects fire one by one, building tension.
- Dice modifications should be visually distinct — gold dice, glowing dice, cracked cursed dice, etc.
- Boss encounters should have unique visual theming and an intimidating score counter.

### Accessibility
- Color-blind mode for dice modifications (use patterns/symbols in addition to colors).
- Option to slow down or skip scoring animations.
- Clear tooltips for all Charms, Enchantments, and enemy effects.

---

## Scoring Sequence (Detailed)

When the player clicks "Score," the following happens in order:

1. **Determine combination** — Check which scoring category the played dice form.
2. **Calculate base chips** — Sum of scored dice faces + category's chip bonus (from Blessings).
3. **Calculate base mult** — Category's mult value (from Blessings).
4. **"On Score" Charms trigger** — For each scored die, left to right, apply any On Score Charm effects. (This is where retriggers from Lucky/Echoing Die happen.)
5. **"On Category" Charms trigger** — Apply any Charms that react to the specific category scored.
6. **"Independent" Charms trigger** — Apply flat bonuses from left to right across the Charm slots.
7. **Die Modification effects** — Apply Gilded chips, Void mult, Steel mult (for held dice), Mirrored mult, Cursed mult.
8. **Enemy passive applied** — If the enemy modifies scoring, apply it now.
9. **Final calculation** — Total Chips × Total Mult = Score for this hand.
10. **Add to cumulative score** — Check if target is met.

**Order matters.** Additive mult (+mult) should resolve before multiplicative mult (×mult), just like Balatro. Charm slot order (left to right) determines activation sequence, giving the player control over optimization.

---

## Balancing Principles

- **Trial 1** should be beatable with minimal Charms and no Blessings. It teaches the mechanics.
- **Trial 2** requires a basic build direction — the player should have a preferred category and a few synergistic Charms.
- **Trial 3** is the mid-game check. Players without a coherent build will stall here. Scaling Charms become essential.
- **Trial 4** demands exponential scaling. ×mult Charms and heavily leveled categories are necessary.
- **Trial 5** is the victory lap for strong builds and a wall for mediocre ones. Boss modifier is designed to be the hardest challenge in the game.
- Boss encounters should feel like "can my build handle this specific restriction?" rather than "is my score high enough?" — the modifier should force adaptation.

---

## Technical Considerations

- **RNG seeding:** Each run should have a seed for reproducibility and sharing.
- **Save system:** Save state after each encounter. One save slot per run (roguelike).
- **Animation system:** The scoring sequence animation is critical to game feel. Budget significant time for juice/polish.
- **Charm interaction testing:** With 30+ Charms, combinatorial interactions need thorough testing. Edge cases with retriggers, scaling, and enemy passives interacting should be documented and tested.

---

## Future Expansion Ideas

- **Endless Mode:** After Trial 5, continue with procedurally generated Trials of increasing difficulty.
- **Daily Challenge:** Seeded runs with preset starting conditions and leaderboards.
- **New Charm sets** added per content update.
- **Multiplayer mode:** Two players race to beat the same enemies with the same seed.
- **Custom Dice:** Unlock cosmetic dice skins and materials.
- **8-sided Dice Set:** Unlockable Dice Set that uses d8s instead of d6s. All scoring thresholds and categories adjusted.
