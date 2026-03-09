Game Setup

Set secret_word to a chosen word (converted to uppercase)
Set max_incorrect to 6
Set incorrect_guesses to 0
Set guessed_letters to an empty collection
Set current_state to "PLAYING"
Main Game Loop

While current_state is "PLAYING":

1. Display the Board
For each letter in secret_word:
If the letter is in guessed_letters:
Display the letter
Else:
Display "_"
Display "Mistakes: " + incorrect_guesses + " / " + max_incorrect

2. Get and Validate Input
Prompt the user to guess a letter
Set guess to the user's input (converted to uppercase)

If guess is not a single alphabetical letter:
Display "Invalid input. Please enter a single letter."
Restart the loop from the beginning

If guess is already in guessed_letters:
Display "You already guessed that letter. Try again."
Restart the loop from the beginning

3. Process the Guess
Add guess to guessed_letters

If guess is in secret_word:
Display "Good guess!"
Else:
Display "Incorrect guess."
Increase incorrect_guesses by 1

4. Evaluate Game State (The Invariants)
If incorrect_guesses equals max_incorrect:
Set current_state to "LOST"

Set all_letters_guessed to True
For each letter in secret_word:
If letter is not in guessed_letters:
Set all_letters_guessed to False

If all_letters_guessed is True:
Set current_state to "WON"
Game Over Handling

If current_state is "WON":
Display "Congratulations! You survived. The word was: " + secret_word

If current_state is "LOST":
Display "Game Over! You've been hung. The word was: " + secret_word