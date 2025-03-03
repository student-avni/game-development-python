# game-development-python
import random

def get_word():
    words = ['python', 'hangman', 'developer', 'challenge', 'programming']
    return random.choice(words).upper()

HANGMAN_PICS = [
    """
       +---+
       |   |
           |
           |
           |
           |
    =========
    """,
    """
       +---+
       |   |
       O   |
           |
           |
           |
    =========
    """,
    """
       +---+
       |   |
       O   |
       |   |
           |
           |
    =========
    """,
    """
       +---+
       |   |
       O   |
      /|   |
           |
           |
    =========
    """,
    """
       +---+
       |   |
       O   |
      /|\  |
           |
           |
    =========
    """,
    """
       +---+
       |   |
       O   |
      /|\  |
      /    |
           |
    =========
    """,
    """
       +---+
       |   |
       O   |
      /|\  |
      / \  |
           |
    ========= GAME OVER
    """
]

def display_game(word, guessed_letters, attempts):
    print(HANGMAN_PICS[attempts])
    display_word = " ".join([letter if letter in guessed_letters else "_" for letter in word])
    print(f"Word: {display_word}")
    print(f"Guessed Letters: {', '.join(guessed_letters)}")
    print(f"Attempts Left: {len(HANGMAN_PICS) - 1 - attempts}\n")

def play_hangman():
    word = get_word()
    guessed_letters = set()
    attempts = 0

    while attempts < len(HANGMAN_PICS) - 1:
        display_game(word, guessed_letters, attempts)
        guess = input("Guess a letter: ").upper()

        if guess in guessed_letters:
            print("You already guessed that letter. Try again.")
            continue

        guessed_letters.add(guess)
        
        if guess not in word:
            attempts += 1

        if all(letter in guessed_letters for letter in word):
            print(f"Congratulations! You guessed the word: {word}")
            return
    
    display_game(word, guessed_letters, attempts)
    print(f"You lost! The word was: {word}")

if __name__ == "__main__":
    play_hangman()
