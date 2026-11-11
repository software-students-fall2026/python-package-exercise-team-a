[![GitHub Actions](https://github.com/software-students-fall2026/python-package-exercise-team-a/actions/workflows/python-tests.yml/badge.svg)](https://github.com/software-students-fall2026/python-package-exercise-team-a/actions/workflows/python-tests.yml)

# Team A Games Package

A Python package containing five mini-games developed by Team A
for the Python Package Exercise.

The package includes Hangman, Tetris, Wordle, 2048, and Blackjack.
Each game provides a different gameplay experience, from word
guessing and card games to puzzles and arcade-style challenges.

## PyPI Package

Our package is publicly available on PyPI:

[Team A Games Package v0.1.0](https://pypi.org/project/team-a-games-package/0.1.0/)

Install the package using pip:

```bash
pip install team-a-games-package==0.1.0
```

## How to Play

After installing the package, you can launch each game directly
from your terminal.

### 1. Hangman

A word-guessing game where players attempt to uncover a hidden
word by guessing letters.

```bash
play_hangman
```

### 2. Tetris

An arcade-style puzzle game where players arrange falling blocks
to complete horizontal lines.

```bash
play_tetris
```

### 3. Wordle

A word puzzle where players try to guess a five-letter word
using feedback from previous guesses.

```bash
play_wordle
```

### 4. 2048

A number puzzle where players combine matching tiles to reach
the number 2048.

```bash
play_2048
```

### 5. Blackjack

A card game where players compete against the dealer, aiming
to reach a hand value closer to 21 without exceeding it.

```bash
play_blackjack
```

### Requirements

- Python 3.11 or newer
- A terminal or command-line interface
- A graphical desktop environment for games with graphical interfaces

The package installs its required Python dependencies automatically
when installed using pip.

### Additional Notes

Hangman requires Tkinter, and Tetris requires Pygame.
Graphical games must be run in a desktop environment.

No API keys, databases, environment variables, or
additional configuration files are required.

## Developer Documentation

In addition to launching games through the terminal, developers
can import functions from the package into their own Python programs.

### Hangman

The Hangman module provides functions for selecting words,
checking guesses, displaying progress, and determining game status.

**`choose_word(difficulty, category)`**

Selects a word based on the specified difficulty and category.

**`check_guess(word, letter, guessed_letters)`**

Checks a player's guessed letter against the secret word.

**`display_word(word, guessed_letters)`**

Displays the word's progress based on the letters guessed so far.

**`check_game_status(word, guessed_letters, max_attempts=9)`**

Determines the current game status based on the guessed letters
and maximum number of allowed attempts.

**`start_game()`**

Launches the interactive Hangman game.

#### Example

```python
from games_package.hangman import (
    choose_word,
    check_guess,
    display_word,
    check_game_status
)

word = choose_word("easy", "animals")
guessed_letters = []

result = check_guess(word, "a", guessed_letters)

print("Guess result:", result)
print("Word progress:", display_word(word, guessed_letters))
print("Game status:", check_game_status(word, guessed_letters))
```

To launch the full game from Python:

```python
from games_package.hangman import start_game

start_game()
```

### Tetris

The Tetris module provides functions for creating the game board,
managing pieces, checking valid placements, and clearing completed lines.

**`create_board(rows=20, cols=10)`**

Creates an empty Tetris board with the specified number of rows and columns.

**`new_piece(kind, x, y)`**

Creates a Tetris piece of the specified shape at position `(x, y)`.

**`placement_test(board, piece)`**

Checks whether a piece can be placed at its current position on the board.
Returns `True` or `False`.

**`rotate_piece(piece, direction="cw")`**

Rotates a piece in the specified direction. The default is clockwise.

**`drop_piece(board, piece)`**

Moves a piece downward to its lowest valid position.

**`lock_piece(board, piece)`**

Places a piece permanently onto the board.

**`clear_lines(board)`**

Removes completed horizontal lines and returns the updated board
and the number of lines cleared.

**`main()`**

Launches the interactive Tetris game using Pygame.

#### Example

```python
from games_package.tetris_logic import (
    create_board,
    new_piece,
    placement_test,
    rotate_piece,
    drop_piece,
    lock_piece,
    clear_lines
)

board = create_board(20, 10)
piece = new_piece("T", 3, 0)

print("Can place piece:", placement_test(board, piece))

rotated_piece = rotate_piece(piece, "cw")
print("Rotated piece:", rotated_piece)

dropped_piece = drop_piece(board, piece)
print("Dropped piece:", dropped_piece)

board = lock_piece(board, dropped_piece)
board, lines_cleared = clear_lines(board)

print("Lines cleared:", lines_cleared)
```

To launch the full game from Python:

```python
from games_package.tetris import main

main()
```

### Wordle

The Wordle module provides functions for validating words,
selecting secret words, evaluating guesses, and displaying feedback.

**`_is_valid_word(word)`**

Checks whether a word is valid for the game.

**`_choose_word(words, rng=None)`**

Selects a secret word from a collection of possible words.
The optional `rng` parameter allows a custom random number generator.

**`_score_guess(secret, guess)`**

Compares a player's guess against the secret word and returns
feedback indicating which letters are correct, misplaced, or absent.

**`_format_feedback(guess, statuses)`**

Formats the feedback from a guess into a readable representation.

**`play_wordle(max_attempts=6, *, words=None, secret=None, input_fn=input, output_fn=print, rng=None)`**

Launches the interactive Wordle game.

Optional parameters allow developers to customize the maximum
number of attempts, word collection, secret word, input/output
functions, and random number generator.

#### Example

```python
from games_package.wordle import (
    _is_valid_word,
    _choose_word,
    _score_guess,
    _format_feedback
)

print("Valid word:", _is_valid_word("apple"))

word = _choose_word(["apple", "grape", "peach"])
print("Selected word:", word)

secret = "apple"
guess = "grape"

statuses = _score_guess(secret, guess)

print("Guess results:", statuses)
print("Formatted feedback:", _format_feedback(guess, statuses))
```

To launch the full game from Python:

```python
from games_package.wordle import play_wordle

play_wordle()
```

### 2048

The 2048 module provides functions for creating the game board,
moving and merging tiles, checking game conditions, and launching
the interactive game.

**`create_board(size=4)`**

Creates an empty square board with the specified size.

**`add_random_tile(board, rng=None)`**

Adds a randomly selected tile to an available position on the board.
The optional `rng` parameter allows a custom random number generator.

**`new_game(size=4, rng=None)`**

Creates a new game board with its initial tiles.

**`move(board, direction)`**

Moves and merges tiles in the specified direction.

Accepts `"left"`, `"right"`, `"up"`, or `"down"`.

Returns two values:
- The updated board.
- The points earned from merging tiles.

**`has_won(board, target=2048)`**

Checks whether the board contains a tile that meets the target value.
Returns `True` or `False`.

**`is_game_over(board)`**

Checks whether any valid moves remain.
Returns `True` when the game is over.

**`play_2048(size=4)`**

Launches the interactive 2048 game using the specified board size.

#### Example

```python
from games_package.game_2048 import (
    create_board,
    add_random_tile,
    new_game,
    move,
    has_won,
    is_game_over
)

board = create_board(4)
print("Empty board:", board)

board = new_game(4)
print("New game:", board)

board = add_random_tile(board)
print("After adding a tile:", board)

board, points = move(board, "left")

print("Updated board:", board)
print("Points earned:", points)

print("Has won:", has_won(board))
print("Game over:", is_game_over(board))
```

To launch the full game from Python:

```python
from games_package.game_2048 import play_2048

play_2048()
```

### Blackjack

The Blackjack module provides functions for creating and shuffling
a deck of cards, calculating hand values, displaying cards, and
playing against a dealer.

**`create_deck()`**

Creates a standard deck of playing cards.

**`shuffle_deck(deck)`**

Shuffles the cards in the provided deck.

**`sum_hand(hand)`**

Calculates the total Blackjack value of a hand, accounting for
the special value of aces.

**`display_hand(hand, hole=False)`**

Displays the cards in a hand.

The optional `hole` parameter controls whether a card is hidden,
which is useful when displaying the dealer's hand.

**`play_blackjack(init_balance=100)`**

Launches the interactive Blackjack game.

The optional `init_balance` parameter sets the player's starting
balance, which defaults to 100.

#### Example

```python
from games_package.blackjack import (
    create_deck,
    shuffle_deck,
    sum_hand,
    display_hand
)

deck = create_deck()
shuffle_deck(deck)

hand = deck[:2]

print("Hand value:", sum_hand(hand))
display_hand(hand)
```

To launch the full game from Python:

```python
from games_package.blackjack import play_blackjack

play_blackjack(init_balance=100)
```

### Example Programs

The repository includes example programs demonstrating how to use
the package's functions:

- [Hangman Example](./examples/demo_hangman.py)
- [Tetris Example](./examples/demo_tetris.py)
- [Wordle Example](./examples/demo_wordle.py)
- [2048 Example](./examples/demo_game_2048.py)
- [Blackjack Example](./examples/demo_blackjack.py)

Each example demonstrates how to use the corresponding game
and its functions.

## Development and Contributing

### 1. Clone the Repository

```bash
git clone https://github.com/software-students-fall2026/python-package-exercise-team-a.git
cd python-package-exercise-team-a
```

### 2. Set Up the Development Environment

This project uses Pipenv to manage its Python environment and dependencies.

Install Pipenv if it is not already installed:

```bash
python3 -m pip install pipenv
```

Install the project dependencies:

```bash
pipenv install --dev
```

Activate the virtual environment:

```bash
pipenv shell
```

Alternatively, run commands using `pipenv run` without activating the environment.

### 3. Install the Package Locally

To install the package in editable mode for development:

```bash
pipenv run python -m pip install -e .
```

This allows developers to test changes to the package without reinstalling it after every modification.

### 4. Run Automated Tests

The project uses pytest to test game functionality.

Run the full test suite:

```bash
pipenv run pytest
```

All tests should pass before submitting changes.

### 5. Build the Package

The project uses the Python `build` tool to generate distribution files.

```bash
pipenv run python -m build
```

This creates a source distribution and a wheel in the `dist/` directory.

### 6. Validate Distribution Files

Use Twine to check the generated distribution files:

```bash
pipenv run python -m twine check dist/*
```

### 7. Publish to PyPI

Authorized maintainers can upload a new package version using Twine:

```bash
pipenv run python -m twine upload dist/*
```

A valid PyPI API token is required to publish.

Before publishing a new release, update the version number in `pyproject.toml` and rebuild the distribution files.

### 8. Contributing Changes

All contributions should follow the team's GitHub workflow:

1. Create a new feature branch from the latest `main` branch.
2. Make and test your changes.
3. Commit and push the feature branch.
4. Open a pull request targeting the team's `main` branch.
5. Wait for GitHub Actions checks and teammate review.
6. Merge the approved pull request.
7. Delete the completed feature branch.
8. Pull the updated `main` branch locally.

Do not commit changes directly to `main`.

## Continuous Integration

GitHub Actions automatically builds and tests the package on
Python 3.11 and Python 3.12 when pull requests are opened against
the `main` branch.

## Team Members

- [Andy Chi](https://github.com/ac11238)
- [Sean Alliman](https://github.com/SeanA12)
- [Tyler Wu](https://github.com/uwtz)
- [Kathy Lin](https://github.com/lkykathy)
- [Monica Lee](https://github.com/monica9482)
