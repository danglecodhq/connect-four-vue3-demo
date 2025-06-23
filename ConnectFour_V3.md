
# 📝 Connect Four Web App Specification Document (V3)

## 1. 🎯 Project Summary

A browser-based, turn-based **Connect Four** game for **3 players** built with **Vue 3**, **TypeScript**, **Vite**, and **Tailwind CSS**. This version supports 3-player alternating turns, win detection, disc drop animation, and enhanced visual feedback.

## 2. 🧑‍💻 Functional Requirements

| ID     | Description                                                              | Priority |
|--------|--------------------------------------------------------------------------|----------|
| FR-01  | Display a 7x6 game grid                                                  | High     |
| FR-02  | Allow 3 players to drop a disc into a column in their turn              | High     |
| FR-03  | Automatically switch turns in order: Red → Yellow → Blue                | High     |
| FR-04  | Detect and announce the winner when four same-color discs align         | High     |
| FR-05  | Highlight result area based on the winner's color                       | Medium   |
| FR-06  | Provide a button to reset the game board                                | High     |
| FR-07  | Prevent additional moves after a win is detected                        | High     |
| FR-08  | Display turn indicator or win message with correct color styling        | Medium   |
| FR-09  | Ensure responsive layout for mobile and desktop                         | High     |
| FR-10  | Ensure disc color and logic supports at least 3 unique players          | High     |
| FR-11  | Animate the disc drop using Vue transitions or CSS                      | Medium   |

## 3. 🤖 Non-Functional Requirements

| ID     | Description                                                | Priority |
|--------|------------------------------------------------------------|----------|
| NFR-01 | Load time under 1 second on desktop                        | High     |
| NFR-02 | No external backend required (fully frontend-based)        | High     |
| NFR-03 | Codebase uses Composition API and TypeScript for structure | High     |
| NFR-04 | Responsive design with Tailwind                             | High     |
| NFR-05 | Accessibility: keyboard focus and screen-reader support    | Medium   |

## 4. 🔄 User Flow

```
[Home / Game Page]
      |
      v
[Initial State: Empty board + “Red's Turn” displayed]
      |
      v
[Player clicks on column]
      |
      v
[Disc drop animation plays as disc falls into lowest empty slot] 👈 NEW
      |
      v
[Check for winner]
     | yes                    | no
     v                       v
[Show "Red/Yellow/Blue Wins"]   [Switch turn → Next player: Red → Yellow → Blue → Red → ...]
      |
      v
[Click "Restart Game"] → [Reset board + turn to Red]
```

## 5. 🎨 UX & UI Design Principles

| Area         | Decision                                                                 |
|--------------|--------------------------------------------------------------------------|
| Color Scheme | Red, Yellow, and Blue discs; Blue grid background                        |
| Clarity      | Turn indicator and win message are color-coded for current player        |
| Feedback     | Disc falls with animation using Vue transitions or CSS                   |
| Layout       | Grid layout using Tailwind, centered and spaced for visibility           |
| Restart      | Reset button visible; clears board and resets turn                       |
| Responsive   | Works on all screen sizes; touch-friendly                                |
| Accessibility| Maintain contrast; consider labels/symbols for clarity                   |
| Animation    | Use CSS keyframes or Vue `<transition>` with transform drop effect       |

## 6. 📊 Requirements Traceability Matrix

| Requirement         | Functional (FR) | Non-Functional (NFR) | Covered in UI | Unit Tested |
|--------------------|------------------|------------------------|----------------|-------------|
| Grid Display        | FR-01           |                        | ✅              | ✅           |
| Drop Logic          | FR-02           |                        | ✅              | ✅           |
| Turn Switching      | FR-03           |                        | ✅              | ✅           |
| Win Check           | FR-04           |                        | ✅              | ✅           |
| Result Display      | FR-05, FR-08    | NFR-05                 | ✅              | ✅           |
| Restart Game        | FR-06           |                        | ✅              | ✅           |
| Win Lockout         | FR-07           |                        | ✅              | ✅           |
| Responsive Layout   |                 | NFR-04                 | ✅              | (Visual)     |
| TypeScript/Composition |             | NFR-03                 | ✅              | ✅           |
| 3rd Player Support  | FR-10           |                        | ✅              | ✅           |
| Disc Animation      | FR-11           |                        | ✅              | ✅           |

## 7. 🧪 Unit Test Scenarios

### ✅ Game Logic Tests

- `dropDisc()` places disc in lowest available row
- Turn order cycles through Red → Yellow → Blue correctly
- Invalid move in full column is ignored
- Win detection works for Red, Yellow, Blue (horizontal, vertical, diagonal)
- Game prevents additional moves after win
- Reset clears board and starts with Red again

### ✅ UI Component Tests

- `GameCell.vue` renders correct color for Red, Yellow, Blue, or null
- `GameBoard.vue` displays correct grid size
- Result area shows win message for each player with proper styles
- Turn display updates as expected
- Restart resets board and state
- `GameCell.vue` applies CSS animation on insert (`drop-enter-active` class)
- `GameCell.vue` renders transition without artifacts (simple enter from above)

## 8. 📦 Future Enhancements

| Feature              | Description                                             |
|----------------------|---------------------------------------------------------|
| AI Opponent          | Add CPU logic using Minimax or random drop             |
| Online Multiplayer   | WebSocket/Supabase channels to enable live play        |
| Sound Effects        | Add drop/win sounds                                     |
| Timer or Move History| Track moves with timestamps                            |
