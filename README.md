import random

def choose_word():
    # You can expand this list or load from a file
    word_list = ["python", "hangman", "internship", "project", "developer", "keyboard", "algorithm"]
    return random.choice(word_list)

def display_current_state(word, guessed_letters):
    display = [letter if letter in guessed_letters else '_' for letter in word]
    return ' '.join(display)

def hangman():
    word = choose_word()
    guessed_letters = []
    incorrect_guesses = 0
    max_attempts = 6

    print("🎯 Welcome to the Hangman Game!")
    print("Guess the word, one letter at a time.")
    print("You have", max_attempts, "incorrect guesses allowed.")

    while incorrect_guesses < max_attempts:
        print("\nWord:", display_current_state(word, guessed_letters))
        print("Guessed Letters:", ' '.join(guessed_letters))

        guess = input("Enter a letter: ").lower()

        if not guess.isalpha() or len(guess) != 1:
            print("⚠ Please enter a single valid alphabet.")
            continue

        if guess in guessed_letters:
            print("⚠ You already guessed that letter.")
            continue

        guessed_letters.append(guess)

        if guess in word:
            print("✅ Good job! The letter is in the word.")
            if set(word).issubset(set(guessed_letters)):
                print("\n🎉 Congratulations! You've guessed the word:", word)
                break
        else:
            incorrect_guesses += 1
            print(f"❌ Wrong guess! Attempts left: {max_attempts - incorrect_guesses}")

    if incorrect_guesses == max_attempts:
        print("\n💀 Game Over! The correct word was:", word)

# Start the game
if _name_ == "_main_":
    hangman()
