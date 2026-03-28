# 🎮 Knapsack Quest

> A browser-based shopping simulation game built on the classic **0/1 Knapsack Problem**, solved with Dynamic Programming.

---

## 📌 Project Overview

**Knapsack Quest** is an interactive single-page web application designed as a college project to demonstrate the **0/1 Knapsack algorithm** through gameplay. Players act as traders with a limited budget of **25 points**, selecting items from a market to maximize their total selling profit. After submitting their selection, the app runs the DP algorithm in the background and tells the player whether they found the optimal solution.

---

## 🚀 How to Run

No installation, no dependencies, no build step required.

1. Download `knapsack_quest.html`
2. Open it in any modern browser (Chrome, Firefox, Edge, Safari)
3. Play instantly

> ✅ Fully self-contained — all HTML, CSS, and JavaScript are in one file.

---

## 🎯 Game Rules

| Parameter | Value |
|-----------|-------|
| Starting Budget | 25 Points |
| Total Items | 10 |
| Goal | Maximize Total Selling Value |

- Each item has a **Buy Value** (cost in points) and a **Sell Value** (profit earned)
- Click an item card to **add it to your cart**; click again to **remove it**
- You **cannot exceed 25 points** — the game blocks and warns you
- Hit **Submit** to evaluate your selection against the algorithmic optimum

---

## 🛒 Item Catalogue

| # | Item | Buy (pts) | Sell (pts) |
|---|------|-----------|------------|
| 1 | 💠 Quantum Chip | 3 | 8 |
| 2 | 🔬 NanoCore | 6 | 14 |
| 3 | ⚡ Photon Cell | 2 | 5 |
| 4 | 💎 CryptoGem | 5 | 12 |
| 5 | 🗄️ Data Vault | 8 | 18 |
| 6 | 🛡️ Ion Shield | 4 | 9 |
| 7 | 🧬 BioSensor | 7 | 15 |
| 8 | 🌌 StarMap | 1 | 3 |
| 9 | 🔴 Plasma Core | 9 | 20 |
| 10 | 🥽 Holo Lens | 6 | 13 |

---

## 🧠 Algorithm — 0/1 Knapsack (Dynamic Programming)

### Problem Statement

Given `n` items each with a `weight` (cost) and `value` (profit), and a knapsack of capacity `W`, find the subset of items that **maximizes total value** without exceeding capacity `W`. Each item can be picked **at most once** (hence "0/1").

### DP Formulation

Define a 2D table:

```
dp[i][w] = maximum profit using the first i items with a budget of w points
```

**Base case:**
```
dp[0][w] = 0  for all w   (no items → no profit)
dp[i][0] = 0  for all i   (no budget → no profit)
```

**Recurrence relation:**
```
if weight[i] > w:
    dp[i][w] = dp[i-1][w]          // item i doesn't fit, skip it

else:
    dp[i][w] = max(
        dp[i-1][w],                // Option A: skip item i
        dp[i-1][w - weight[i]] + value[i]  // Option B: take item i
    )
```

**Answer:** `dp[n][W]` — bottom-right cell of the table.

### Complexity

| Metric | Value |
|--------|-------|
| Time Complexity | O(n × W) |
| Space Complexity | O(n × W) |
| This game: n=10, W=25 | 250 table cells |

### JavaScript Implementation

```javascript
function knapsack(items, capacity) {
  const n = items.length;

  // Build (n+1) × (capacity+1) table filled with 0
  const dp = Array.from({ length: n + 1 }, () =>
    new Array(capacity + 1).fill(0)
  );

  for (let i = 1; i <= n; i++) {
    const { weight, value } = items[i - 1];
    for (let w = 0; w <= capacity; w++) {
      dp[i][w] = dp[i - 1][w];           // default: skip item i
      if (weight <= w) {
        const withItem = dp[i - 1][w - weight] + value;
        if (withItem > dp[i][w]) dp[i][w] = withItem;
      }
    }
  }

  return dp[n][capacity];   // optimal profit
}
```

---

## 🖥️ Features & UI

- **Header** — Title, subtitle, and How-to-Play instructions
- **Live Dashboard** — Real-time Points Used and Total Profit with animated progress bars
- **Item Grid** — 10 interactive cards showing buy/sell values; selected items are highlighted
- **Overflow Guard** — Shake animation + alert message if an item exceeds remaining budget
- **Disabled State** — Items that no longer fit are greyed out automatically
- **Submit Button** — Triggers the DP algorithm and evaluates the player's choice
- **Feedback Messages:**
  - 🎉 **Jackpot** — confetti animation if the player matches the optimal profit
  - 🔍 **Can Do Better** — shows the gap between player profit and the DP maximum
- **Reset Button** — Clears all selections to start fresh

---

## 📁 File Structure

```
knapsack_quest.html     ← entire application (HTML + CSS + JS, single file)
README.md               ← this file
```

---

## 🛠️ Technologies Used

| Technology | Purpose |
|------------|---------|
| HTML5 | Page structure |
| CSS3 | Styling, animations, responsive layout |
| Vanilla JavaScript | Game logic, DOM manipulation |
| Google Fonts (Orbitron, Rajdhani) | Typography |
| Dynamic Programming | Knapsack algorithm |

No frameworks. No libraries. No build tools.

---

## 📚 Academic Context

This project was built to demonstrate:

1. **Algorithm Design** — Translating a classic CS problem into interactive software
2. **Dynamic Programming** — Bottom-up tabulation approach to the 0/1 Knapsack Problem
3. **Frontend Development** — Single-file responsive web application
4. **User Experience** — Making an algorithmic concept approachable through gameplay

---

## 👤 Author

College Project · Algorithm Design & Analysis  
Built with HTML · CSS · Vanilla JavaScript
