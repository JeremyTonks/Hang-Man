# Hang-Man Version 1.0   --- JEREMY TONKS ---

# This is where the Loop begins out of the main Module.
def SETUP():

    # Calling the Module.
    Number_of_games = MENU()
    Words_selected = DICTIONARY(Number_of_games)
    Blank_spaces = CONVERT(Number_of_games, Words_selected)
    GAME(Number_of_games,Words_selected, Blank_spaces)

    #Repeat the process.
    SETUP()
    
###############################################################################

### DONE ###

# This is the game Menu that the user interacts with.
def MENU():
    
    # Clear the Screen.
    os.system("cls") 
    
    #Display what the user can do.
    print("Hang man - Version 1.0")
    print("Type in \"Play\" and press enter to begin the game. Otherwise type in \"Quit\" to leave.")

    #User can type in a resquested input.
    Request = input(">>")
    
    # What is the users' request?

    # Yes they want to play.
    if Request == "play":

        # Set a Standard to a Variable.
        Number_of_games = 0

        # Clear the screen.
        os.system("cls") 

        # When Games is not either "1" , "2" or "3".
        while Number_of_games < 1 or Number_of_games > 3:

            #User can type how many games they want.
            print("Type in \"1\" or \"2\" or \"3\" and press enter to selected how many games you want to play.")
            Number_of_games = int(input(">> "))

        # When the Conditions are true return how many games they want to play.
        return Number_of_games

    # No they want to quit.
    elif Request == "quit":
        os.system(quit)

    # Something went wrong.       
    else:
        MENU()
    
###############################################################################

### DONE ###

# This is the module that picks the words to guess.
def DICTIONARY(Number_of_games):

    # Make a space for each word in the list.
    Words_selected  = [" _ "] * int(Number_of_games) 

    # Each Number is one game, each game needs one word.
    for Number in range(Number_of_games):

        # Find a Random Index of a word in the List that is a Global Set List.
        Selected_word_index = random.randrange(len(SET_LIST))

        # Use that Index to pick that word, put that word into a selected list.
        Words_selected[Number] = SET_LIST[Selected_word_index]

    # That selected list now needs to be returned.
    return Words_selected

###############################################################################  

### DONE ###

# This is the Module that converts the words so it is hidden.
def CONVERT(Number_of_games, Words_selected):

    # Create a list which makes a place for all the words needed.
    Blank_spaces = [" _ "] * Number_of_games

    # Each Number is one game, each game needs one word.
    for Number in range(Number_of_games):

        # Change each letter into a underscore and put it in a list.
        Blank_spaces[Number] = [" _ "] * len(Words_selected[Number])

    #That Blank Spaces of a list needs to be return.
    return Blank_spaces

############################################################################### 

### WORKING ###       NEEDS A LOSING CONDITION....

# The module is the game.
def GAME(Number_of_games,Words_selected, Blank_spaces):

    # Selected the word from the selected list for this game.
    for Number in range(Number_of_games):
        Word = Words_selected[Number]
        Blank = Blank_spaces[Number]

        # Create a list to show that the user has guessed.
        Users_Guess = []

        # Set the Lives as a Changable Variable.
        Lives = SET_CHANCES

        #While the word hasn't been Completed continue.
        while Blank.__contains__(" _ ") == True:

            # Clear the Screen.
            os.system("cls")

            # Display Information.
            print("Letters Guessed:       Lives Left: {}".format(Lives))
            print("".join(Users_Guess) , "\n")

            # Display Information.
            print("Type in letters and press enter to see if you are correct.")
            print("".join(Blank))

            # Let the user guess a letter.
            guess = input(">> ")

            # Is the guessed letter in the word?
            if Word.__contains__(guess) == True:

                # Look at each letter and see if that letter is in that index placing.
                for Letter_index in range(len(Word)):

                    # if it is, change it to the guessed letter.
                    if guess == Word[Letter_index]:
                        Blank[Letter_index] = guess
                        Users_Guess.append(guess)

                        # Did they get the word done?
                        if Blank.__contains__(" _ ") == False:

                            # Clear the Screen.
                            os.system("cls")

                            # Display if the User got the word correct.
                            print("Bravo the word was {}.".format(Word))
                            input(">> ")

############################################################################### 

### Done ###

# Import the Basic Functions.
import os
import sys
import random

# These will stay the same so they can be Global Variables.
global SET_LIST
global SET_CHANCES

# This is the list of words we are using.
SET_LIST = ["amphibian" , "apocalypse" , "advertisement" , "concludsion" , "combustible" , "carnivorous" , "diplomatic" , "dimensional" , "protection" ]
SET_CHANCES = 10

# Start a Loop for the Game
SETUP()

