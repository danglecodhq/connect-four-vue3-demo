# 📝 Connect Four Web App Specification Document (V1)

## 1. 🎯 Project Summary

A browser-based, two-player **Connect Four** game built with **Vue 3**, **TypeScript**, **Vite**, and **Tailwind CSS**. This game is designed for responsive play with intuitive UI, and includes basic game rules, turn-taking logic, win detection, and a polished UX.

## 2. 🧑‍💻 Functional Requirements

| ID    | Description                                              | Priority |
| ----- | -------------------------------------------------------- | -------- |
| FR-01 | Display a 7x6 game grid                                  | High     |
| FR-02 | Allow players to drop a disc into a column on their turn | High     |
| FR-03 | Automatically switch turns after a move                  | High     |
| FR-04 | Detect and announce the winner when four discs align     | High     |
| FR-05 | Highlight the result area based on winner color          | Medium   |
| FR-06 | Provide a button to reset the game board                 | High     |
| FR-07 | Prevent additional moves after a win is detected         | High     |
| FR-08 | Display turn indicator or win message with color cues    | Medium   |
| FR-09 | Ensure responsive layout for mobile and desktop          | High     |

## 3. 🤖 Non-Functional Requirements

| ID     | Description                                                | Priority |
| ------ | ---------------------------------------------------------- | -------- |
| NFR-01 | Load time under 1 second on desktop                        | High     |
| NFR-02 | No external backend required (fully frontend-based)        | High     |
| NFR-03 | Codebase uses Composition API and TypeScript for structure | High     |
| NFR-04 | Responsive design with Tailwind                            | High     |
| NFR-05 | Accessibility: keyboard focus and screen-reader support    | Medium   |

## 4. 🔄 User Flow

```
[Home / Game Page]
      |
      v
[Initial State: Empty board + “Red's Turn” displayed]
      |
      v
[Player clicks on column] -> [Disc drops to lowest empty slot]
      |
      v
[Check for winner]
     | yes                  | no
     v                     v
[Show "Red/Yellow Wins"]   [Switch turn -> Update turn indicator]
      |
      v
[Click "Restart Game"] -> [Reset board + turn to Red]
```

## 5. 🎨 UX & UI Design Principles

| Area         | Decision                                                              |
| ------------ | --------------------------------------------------------------------- |
| Color Scheme | Red vs Yellow discs, Blue grid background                             |
| Clarity      | Turn indicator or win result highlighted with background + color text |
| Feedback     | Disc visually drops (instant or animated later), interactive cursor   |
| Layout       | Grid-based layout using Tailwind `grid-cols-7`, centered on screen    |
| Restart      | Clear button, accessible after game ends or anytime                   |
| Responsive   | Optimized for small and large screens, tap-friendly cell hitboxes     |

## 6. 📊 Requirements Traceability Matrix

| Requirement  | Functional (FR) | Non-Functional (NFR) | Covered in UI | Unit Tested   |
| ------------ | --------------- | -------------------- | ------------- | ------------- |
| Grid Display | FR-01           |                      | ✅            | ✅            |
| Drop Logic   | FR-02           |                      | ✅            | ✅            |
| Turn Switch  | FR-03           |                      | ✅            | ✅            |
| Win Check    | FR-04           |                      | ✅            | ✅            |
| Result Area  | FR-05, FR-08    | NFR-05               | ✅            | ✅            |
| Restart      | FR-06           |                      | ✅            | ✅            |
| Win Freeze   | FR-07           |                      | ✅            | ✅            |
| Responsive   |                 | NFR-04               | ✅            | (Visual)      |
| TypeScript   |                 | NFR-03               | N/A           | ✅ (TS types) |

## 7. 🧪 Unit Test Scenarios

Framework suggestion: **Vitest** or **Jest**

### ✅ Game Logic Tests (Composable or `GameBoard.vue`)

- `dropDisc()` places disc in lowest available row
- turn switches after a move
- invalid move in full column is ignored
- win detection (horizontal, vertical, diagonal)
- no further moves after win
- reset clears board and sets player to red

### ✅ UI Component Tests

- `GameCell.vue` renders correct color based on prop
- `GameBoard.vue` renders 6x7 grid
- result text displays correctly on win
- restart button resets board

## 8. 📦 Future Enhancements

| Feature               | Description                                     |
| --------------------- | ----------------------------------------------- |
| AI Opponent           | Add CPU logic using Minimax or random drop      |
| Disc Drop Animation   | Use Vue transitions or CSS animation            |
| Online Multiplayer    | WebSocket/Supabase channels to enable live play |
| Sound Effects         | Add drop/win sounds                             |
| Timer or Move History | Track moves with timestamps                     |
