"""
from tkinter import *  
from tkinter import messagebox
import random


class Player():
    def __init__(self):
        self.counter = 1

    def name(self, name):
        self.name = name

    def name(self):
        return self.name

    def count(self):
        self.counter += 1
        return self.counter


class default():
    def __init__(self, name, win1, win2):
        self.name = name
        self.dic = {win1, win2}


Scissors = default('Scissors', 'Paper', 'Lizard')
Paper = default('Paper', 'Spock', 'Rock')
Rock = default('Rock', 'Lizard', 'Scissors')
Lizard = default('Lizard', 'Paper', 'Spock')
Spock = default('Spock', 'Scissors', 'Rock')

newPlayer = Player()


def welcomePlayer(event):
    newPlayer.name = str(nameEntry.get())
    messagebox.showinfo("", "welcome " + str(newPlayer.name))
    nameWindow.destroy()  # close window
    playWindow()  # open two other windows, one is to display result, anther is use to play game


def playWindow():
    def close(event):
        messagebox.showinfo("Thanks", "Thanks for using")
        gameWindow.destroy()
        scoreboardWindow.destroy()

    gameWindow = Tk()
    gameWindow.geometry('400x220')
    gameWindow.title('Game')
    playerNameLabel = Label(
        gameWindow,
        text="Player: " + newPlayer.name
    )
    playerNameLabel.pack(side=TOP)

    def fightWiner(event):  # obj1 is human, obj2 is NPC
        nowCount = newPlayer.count()

        if nowCount > 6:
            finishWindow = Tk()
            finishWindow.title('Finish!')

            '''
            if playerWin > NPC_Win:
                winnerInfo = 'Player Win!'
            elif NPC_Win > playerWin:
                winnerInfo = 'NPC Win!'
            else:
                winnerInfo = "Draw"
            '''

            winnerLabel = Label(
                finishWindow,
                # text = winnerInfo
                text="Win"
            )
            winnerLabel.pack(side=TOP)
            # -- EXIT BUTTON --
            exitButton = Button(
                finishWindow,
                text="EXIT"
            )
            exitButton.bind("<Button-1>", close)
            exitButton.pack(side=TOP)

            finishWindow.mainloop()

        timesListbox.insert(nowCount, str(nowCount - 1) + 'st')
        playerChoice = var.get()
        if playerChoice == 1:
            obj1 = Scissors
        elif playerChoice == 2:
            obj1 = Paper
        elif playerChoice == 3:
            obj1 = Rock
        elif playerChoice == 4:
            obj1 = Lizard
        elif playerChoice == 5:
            obj1 = Spock
        playerChooseListbox.insert(nowCount, obj1.name)

        NPC_Choice = random.randint(1, 5)
        if NPC_Choice == 1:
            obj2 = Scissors
        elif NPC_Choice == 2:
            obj2 = Paper
        elif NPC_Choice == 3:
            obj2 = Rock
        elif NPC_Choice == 4:
            obj2 = Lizard
        elif NPC_Choice == 5:
            obj2 = Spock
        NPC_ChooseListbox.insert(nowCount, obj2.name)

        if obj1.name == obj2.name:
            result = "Draw"
        elif obj2.name in obj1.dic:
            result = (str(newPlayer.name) + " Win")

        else:
            result = ("NPC Win")

        resultListbox.insert(nowCount, result)

    var = IntVar()

    radioScissors = Radiobutton(
        gameWindow,
        text='Scissors',
        variable=var,
        value=1,
    )
    radioScissors.pack(side=TOP)

    radioPaper = Radiobutton(
        gameWindow,
        text='Paper',
        variable=var,
        value=2,
    )
    radioPaper.pack(side=TOP)

    radioRock = Radiobutton(
        gameWindow,
        text='Rock',
        variable=var,
        value=3,
    )
    radioRock.pack(side=TOP)

    radioLizard = Radiobutton(
        gameWindow,
        text='Lizard',
        variable=var,
        value=4,
    )
    radioLizard.pack(side=TOP)

    radioSpock = Radiobutton(
        gameWindow,
        text='Spock',
        variable=var,
        value=5,
    )
    radioSpock.pack(side=TOP)

    # -- scoreboard --
    scoreboardWindow = Tk()
    scoreboardWindow.title('Scoreboard')

    # -- Times --
    timesListbox = Listbox(scoreboardWindow)
    timesListbox.insert(1, "Times:")

    timesListbox.pack(side=LEFT)

    # -- Player Choose --
    playerChooseListbox = Listbox(scoreboardWindow)
    playerChooseListbox.insert(1, "Player Choose:")

    playerChooseListbox.pack(side=LEFT)

    # -- NPC Choose --
    NPC_ChooseListbox = Listbox(scoreboardWindow)
    NPC_ChooseListbox.insert(1, "NPC Choose:")

    NPC_ChooseListbox.pack(side=LEFT)

    # -- Result --
    resultListbox = Listbox(scoreboardWindow)
    resultListbox.insert(1, "Result:")

    resultListbox.pack(side=LEFT)

    submitButton = Button(
        gameWindow,
        text="Start"
    )
    submitButton.bind("<Button-1>", fightWiner)
    submitButton.pack(side=TOP)


# -- Name Window --
nameWindow = Tk()
nameWindow.title("Name")

tipLabel = Label(
    nameWindow,
    text='Please enter your name: '
)
tipLabel.pack(side=LEFT)

nameEntry = Entry(nameWindow)
nameEntry.pack(side=LEFT)

nameButton = Button(nameWindow, text='Submit')
nameButton.bind("<Button-1>", welcomePlayer)
nameButton.pack(side=LEFT)

# -- Start --
nameWindow.mainloop()
