import random
import string

vowels = 'aeiou'
consonants = 'bcdfghjklmnpqrstvwxyz'
handsize = 0

lettervalues = {
    'a': 1, 'b': 3, 'c': 3, 'd': 2, 'e': 1, 'f': 4, 'g': 2, 'h': 4, 'i': 1, 'j': 8, 'k': 5, 'l': 1, 'm': 3, 'n': 1, 'o': 1, 'p': 3, 'q': 10, 'r': 1, 's': 1, 't': 1, 'u': 1, 'v': 4, 'w': 4, 'x': 8, 'y': 4, 'z': 10
}
wordlist = "words.txt"
def loadWords():
    inFile = open(wordlist, 'r', 1)
    wordList = []
    for line in inFile:
        wordList.append(line.strip().lower())
    return wordList
def getFrequencyDict(sequence):
    frequency = {}
    for x in sequence:
        frequency[x] = frequency.get(x,0) + 1
    return frequency
loadWords()
def getWordScore(word, n):
    length=len(word)
    word=word.lower()
    score=0
    for ch in word:
        score+=lettervalues[ch]
    score*=length
    if(length==n):
        score+=50
    return score
def displayHand(hand):
    hands = []
    for letter in hand.keys():
        for j in range(hand[letter]):
             hands.append(letter)
    print(hands)

def dealHand(n):
    hand = {}
    numVowels = int(n / 3)

    for i in range(numVowels):
        x = vowels[random.randrange(0, len(vowels))]
        hand[x] = hand.get(x, 0) + 1

    for i in range(numVowels, n):
        x = consonants[random.randrange(0, len(consonants))]
        hand[x] = hand.get(x, 0) + 1
    return hand

def updateHand(hand,word):
    hand_copy=dict(hand)
    for ch in word:
        hand_copy[ch]=hand_copy.get(ch,0)-1
        if(hand_copy.get(ch,0)==0):
            del hand_copy[ch]
    return hand_copy

def isValidWord(word, hand, wordList):
    wordlist_copy = wordList[:]
    hand_copy = hand.copy()
    flag = 1
    if word in wordlist_copy:
        for ch in word:
            if ch in hand_copy:
                flag = 0
                hand_copy[ch] = hand_copy.get(ch, 0) - 1
                if (hand_copy.get(ch, 0) == 0):
                    del hand_copy[ch]
            else:
                flag = 1
                break
    if (flag == 0):
        return True
    else:
        return False

def calculateHandLength(hand):
    counter = 0
    for ch in hand:
        if (hand.get(ch,0)>0):
            counter += 1
    return counter


def playHand(hand, wordList, n):
    score = 0
    while (calculateHandLength(hand) > 0):
        print("Current Hand: ", end="")
        displayHand(hand)

        word = input('Enter word, or a "." to indicate that you are finished: ')
        if (word == "."):
            print("Goodbye! Total score: ", score, " points")
            break
        else:
            if not isValidWord(word, hand, wordList):
                print("Invalid word, please try again.")
                continue
            else:
                score1 = getWordScore(word, n)
                score += score1
                print('"' + str(word) + '"' + " earned " + str(score1) + " points. Total: " + str(score) + " points.")
                hand = updateHand(hand, word)
    if (calculateHandLength(hand) == 0):
        print("Run out of letters. Total score: " + str(score) + " points.")
def playGame(wordList):
    hand = {}
    HAND_SIZE = 9
    while True:
        choice = input("Enter n to deal a new hand, r to replay the last hand, or e to end game: ")
        if (choice == 'n'):
            hand = dealHand(HAND_SIZE)
            playHand(hand, wordList, HAND_SIZE)
        elif (choice == 'r'):
            if (hand == {}):
                print("You have not played a hand yet. Please play a new hand first!")
            else:
                hand = hand.copy()
                playHand(hand, wordList, HAND_SIZE)
        elif (choice == 'e'):
            break
        else:
            print("Invalid command.")
            continue
if __name__ == '__main__':
    wordList = loadWords()
    playGame(wordList)

