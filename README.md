# Online Multiplayer Card Game "Idiot"

## 1. Game Design

### Game Overview

- **Name**: Idiot
- **Objective**: Be the first player to lose all your cards
- **Players**: 2-6

### Game Rules

1. ##### Setup: Players start with 3 cards in hand, 3 face-up, and 3 face-down

    - Use 2 standard deck of cards (No jokers/wilds)
    - Deal 3 face-down cards to each player (not to be looked at)
    - Deal 6 more cards to each player
    - Players choose 3 of these 6 cards to place face-up on their face-down cards

2. ##### Gameplay:

    - Start: Player with the lowest card (usually a 3) begins

    - Turn order: Fixed clockwise player rotation

    - Playing cards: Must be equal or higher than the top card of the pile

    - Drawing: After playing, draw to maintain 3 cards in hand until deck is empty

    - Picking up: If unable to play, pick up the entire pile

3. ##### Special Cards:

    - 2: Can be played on any card, resets the pile (any card can be played next)

    - 10: Burns the pile (discards all cards in the pile)

    - Four of a kind: Burns the pile

4. ##### Endgame:

    - Players will continue to drain cards from the draw pile until the draw pile runs out. 

    - Then once players finish their in-hand cards, they can pick a card from their 3 face-up cards

    - Finally, once their 3 face-up cards are played, players can pick and play a face-down card (this is a blind-flip, players will not be able to see the coat or number of the card they are picking until after they pick it)

## 2. User Interface Layout

### Game Screen Layout

- Player Arrangement
    - Players positioned in a circular formation around a central play area
    - Current player clearly highlighted with visual indicator (glow, star, etc.)
    - Turn direction indicated with arrow showing clockwise rotation
- Player Display Elements
    - Username displayed prominently
    - Visual representation of 2 card zones per player
        1. Hand cards (3 cards, visible only to the player)
        2. On table cards:
            - 3 cards, visible to all players sitting ontop of;
            - 3 Face-down cards (backs showing until played)
- Central Game Elements
    - Current play pile with visible top card
    - Discard pile (for burned cards)
    - Remaining draw-deck with card count
    - Turn indicator showing whose turn it is
- UI Controls
    - Card selection mechanism
    - Play button for selected card(s)
    - Skip/pickup pile button when unable to play
    - Game rules reference toggle

## 3. Technical Implementation

### User Authentication & Room Management

- User Identification
    - Players receive default guest IDs (e.g., "Guest4839") upon site visit
    - Optional nickname customization before joining/creating rooms
    - No mandatory account creation for basic gameplay
    - Session tokens maintain temporary identity between page refreshes
- Room Creation & Management
    - Creation Flow
        - Player enters nickname
        - Player creates room with optional custom name (default: "[Username]'s room")
        - Player selects privacy setting (public/private)
        - Private rooms generate a unique 6-digit access code
    - Room Discovery
        - Public rooms visible in a browsable lobby
        - Private rooms accessible only via direct code entry
        - Recently active rooms displayed prominently
- Room States
    - Waiting lobby: Where players gather before game starts
    - Active game: When gameplay is in progress
    - Post-game: Displays results and offers rematch option

### Technology Stack

- **Frontend**: JavaScript/TypeScript with React
- **Backend**: Node.js with Express
- **Real-time Communication**: Socket.IO
- **State Management**: Redux for frontend, server-side game state

### Key Technical Requirements

- Real-time Synchronization
    - Card movements must be visible to all players simultaneously
    - Game state updates pushed to all connected clients
    - Optimistic UI updates with server validation
- State Management
    - Central authoritative game state on server
    - Client-side prediction for responsive UI
    - Reconciliation for handling network latency
- Persistence
    - Game continues if players disconnect temporarily
    - Ability for players to rejoin in-progress games
    - Game state snapshot storage for recovery
- Scalability
    - Independent game rooms that don't affect each other
    - Ability to handle multiple concurrent game sessions
    - Efficient resource usage for longer gameplay sessions
- User Experience
    - Clear visual indication of turn order and current player
    - Animated card movements for better gameplay understanding
    - Mobile-responsive design for cross-device play
