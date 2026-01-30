# Nim AI

Train an AI to master the game of Nim using Q-learning reinforcement learning. The AI plays thousands of games against itself, learns the optimal strategy, and becomes impossible to beat. Try your luck against it.

## About the Game

Nim is a mathematical strategy game where two players take turns removing objects from distinct piles. On each turn, a player must remove at least one object from a single pile. The player who takes the last object loses the game.

This implementation uses the classic configuration of 4 piles with 1, 3, 5, and 7 objects respectively.

## How It Works

The AI uses **Q-learning**, a model-free reinforcement learning algorithm, to learn the optimal strategy:

- **State**: The current configuration of piles (e.g., `(1, 3, 5, 7)`)
- **Action**: A tuple `(pile_index, count)` representing removing `count` objects from pile `pile_index`
- **Reward**: +1 for winning, -1 for losing, 0 for ongoing moves
- **Learning Rate (alpha)**: Controls how much new information overrides old information
- **Exploration Rate (epsilon)**: Probability of choosing a random action vs the best known action

The AI trains by playing thousands of games against itself, gradually learning which moves lead to victories.

## Installation

1. Clone the repository:
```bash
git clone https://github.com/0xFazal/nim-ai.git
cd nim-ai
```

2. Ensure you have Python 3.6+ installed. No external dependencies are required.

## Usage

### Quick Start

Run the game with the default training of 10,000 games:

```bash
python play.py
```

### Custom Training

You can customize the training and gameplay in Python:

```python
from nim import train, play

# Train the AI with a custom number of games
ai = train(50000)

# Play against the AI (random turn order)
play(ai)

# Play against the AI as the first player
play(ai, human_player=0)

# Play against the AI as the second player
play(ai, human_player=1)
```

### Adjusting AI Parameters

```python
from nim import NimAI, Nim

# Create AI with custom learning parameters
ai = NimAI(alpha=0.5, epsilon=0.1)

# alpha: learning rate (0.0 to 1.0)
# epsilon: exploration rate (0.0 to 1.0)
```

## Project Structure

```
nim/
├── nim.py      # Core game logic and AI implementation
├── play.py     # Entry point for playing the game
└── README.md
```

### Module Overview

**nim.py** contains:

- `Nim`: The game class managing state, moves, and win conditions
- `NimAI`: The Q-learning AI implementation
- `train(n)`: Function to train the AI over `n` games
- `play(ai, human_player)`: Function to play against a trained AI

## Gameplay Example

```
Piles:
Pile 0: 1
Pile 1: 3
Pile 2: 5
Pile 3: 7

AI's Turn
AI chose to take 2 from pile 3.

Piles:
Pile 0: 1
Pile 1: 3
Pile 2: 5
Pile 3: 5

Your Turn
Choose Pile: 2
Choose Count: 3
```

## Technical Details

### Q-Learning Formula

The AI updates Q-values using the standard Q-learning update rule:

```
Q(s, a) = Q(s, a) + alpha * (reward + max(Q(s', a')) - Q(s, a))
```

Where:
- `s` is the current state
- `a` is the action taken
- `s'` is the resulting state
- `alpha` is the learning rate

### Strategy

After sufficient training, the AI learns to exploit the mathematical properties of Nim. The optimal strategy involves calculating the XOR (nim-sum) of all pile sizes and making moves to create advantageous positions.

## License

This project is open source and available under the MIT License.
