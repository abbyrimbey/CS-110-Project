# CS-110-Project
import tkinter
import createList

class MainMenu():
    def __init__(self):

        #Set Up HomeScreen as main window
        self.__homeScreen = tkinter.Tk()
        self.__homeScreen.title("Bingo Game")
        self.__homeScreen.configure(background = "white")
        self.__homeScreen.geometry("7500x1500")

        self.__topFrame = tkinter.Frame()
        self.__topFrame.configure(background = "white")
        self.__midFrame = tkinter.Frame()
        self.__midFrame.configure(background = "white")
        self.__bottomFrame = tkinter.Frame()
        self.__bottomFrame.configure(background = "white")
        self.__topFrame.grid()
        self.__midFrame.grid()
        self.__bottomFrame.grid()
        
        #Build main menu buttons
        self.__mainMenuButtons()

        #Start App
        tkinter.mainloop()

                            ## SCREEN SET UPs ##
    #Bingo Board
    def __createBoard(self):
        row,col = 0,0
        self.buttons = []
        numbersList = createList.readNum()
        for index in range(1,26):
            self.buttons.append(
                tkinter.Button(self.__midFrame, text=str(numbersList[index-1]),\
                               bg = "white", fg="blue", width=15, height = 4, \
                               font = ("bold"), command=lambda \
                               i=index:self.change(i)))
            self.buttons[-1].grid(row=row + 1, column=col)
            col+=1
            if index%5==0:
                row+=1; col=0

        #This part creates the titles for each column
        self.B = tkinter.Label(self.__midFrame, text="B", bg = "blue", \
                               fg = "white", font = ("bold"), width = 15, \
                               height = 5).grid(row = 0, column = 0)
        self.I = tkinter.Label(self.__midFrame, text="I", bg = "blue", \
                               fg = "white", font = ("bold"), width = 15, \
                               height = 5).grid(row=0,column=1)
        self.N = tkinter.Label(self.__midFrame,text="N", bg = "blue", \
                               fg = "white", font = ("bold"), width = 15, \
                               height = 5).grid(row=0,column=2)
        self.G = tkinter.Label(self.__midFrame,text="G", bg = "blue", \
                               fg = "white", font = ("bold"), width = 15, \
                               height = 5)\
                               .grid(row=0,column=3)
        self.O = tkinter.Label(self.__midFrame,text="O", bg = "blue", \
                               fg = "white", font = ("bold"), width = 15, \
                               height = 5).grid(row=0,column=4)
    def change(self,index):
        if self.buttons[index-1]["bg"] =="white":
            self.buttons[index-1].configure( bg = "black", fg="white")
        else:
            self.buttons[index-1].configure( bg = "white", fg="blue")
        
    #Main Menu Buttons
    def __mainMenuButtons(self):
        #title
       self.__bingo = tkinter.Label(self.__topFrame, text = "BINGO", \
                            font = "Broadway 100 bold", bg = "white",\
                            fg = "red", height = 1)
       self.__bingo.grid()
        #background
       self.__image = tkinter.PhotoImage(file = "457705.gif")
       self.__background = tkinter.Label(self.__bottomFrame, \
                                    image = self.__image)
       self.__background.grid()
       #play button
       self.__play = tkinter.Button(self.__midFrame, text = "Play", \
                                    width = 30, height = 1, bg = "white", \
                                    font = "Times 20 bold", \
                                    command = self.__playGame)
       
       self.__play.grid()
       #instructions button
       self.__instructions = tkinter.Button(self.__midFrame, \
                                            text = "How To Play", width = 30,\
                                            height = 1, bg = "white", \
                                            font = "Times 20 bold", \
                                            command = self.__howToPlay)
       self.__instructions.grid(pady = 20)
       #quit button
       self.__quit = tkinter.Button(self.__midFrame, text = "Quit", \
                                    width = 30, height = 1, bg = "white", \
                                    font = "Times 20 bold", \
                                    command = self.__quitGame)
       self.__quit.grid()

    #How to Play
    def __howToPlay(self):
        self.__bingo.destroy()
        self.__background.destroy()
        self.__play.destroy()
        self.__instructions.destroy()
        self.__quit.destroy()
        
    
    #Game Selection: Traditional, Extreme, Blackout, Back Button to HomeScreen  
    def __gameTypes(self): 
        #create "Choose Game" Heading
        self.__gameSelection = tkinter.Label(self.__topFrame, \
                                         text = "  Choose Game", \
                                         font = "Broadway 65 bold", \
                                         bg = "white", height = 1)
        self.__gameSelection.grid()
        #traditional game option
        self.__traditional = tkinter.Button(self.__midFrame, \
                                            text = "Traditional", width = 30, \
                                            height = 1, bg = "blue", \
                                            font = "Times 20 bold", \
                                            command = self.__playTraditional)
        self.__traditional.grid(pady = 20)
        #Extreme Game option
        self.__extreme = tkinter.Button(self.__midFrame, text = "Extreme", \
                                        width = 30, height = 1, bg = "green", \
                                        font = "Times 20 bold", \
                                        command = self.playExtreme)
        self.__extreme.grid()
        #Blackout Game option
        self.__blackout = tkinter.Button(self.__midFrame, text = "Blackout",\
                                         width = 30, height = 1, bg = "yellow",\
                                         font = "Times 20 bold", \
                                         command = self.playBlackout)
        self.__blackout.grid(pady = 20)
        #back button
        self.__gamesToMain = tkinter.Button(self.__midFrame, text = "Back", \
                                            width = 30, height = 1, bg = "red", \
                                            font = "Times 20 bold", \
                                            command = self.__gamesBackToMain)
        self.__gamesToMain.grid()
        

                            ## PLAY BUTTON COMMANDS ##
        
    #Play Button on HomeScreen
    def __playGame(self):
        self.__background.destroy()
        self.__bingo.destroy()
        self.__play.destroy()
        self.__instructions.destroy()
        self.__quit.destroy()
        self.__gameTypes()
        
    #Play Traditional Game
    def __continueTrad(self):
        self.__winsTraditional.destroy()
        self.__anyRow.destroy()
        self.__horizontalBingo.destroy()
        self.__anyColumn.destroy()
        self.__verticalBingo.destroy()
        self.__bothDiagonals.destroy()
        self.__diagonalBingo.destroy()
        self.__playTrad.destroy()
        self.__traditionalToGames.destroy()
        self.__createBoard()

    #Play Extreme Game
    def __continueExt(self):
        self.__winsExtreme.destroy()
        self.__postCardBingo.destroy()
        self.__playExtreme.destroy()
        self.__extremeToGames.destroy()
        self.__createBoard()

    #Play Blackout Game
    def __continueBkout(self):
        self.__winsBkout.destroy()
        self.__blackoutBingo.destroy()
        self.__playBkout.destroy()
        self.__blackoutToGames.destroy()
        self.__createBoard()

                                ## BACK BUTTONS ##
    #Game Selection to HomeScreen
    def __gamesBackToMain(self):
        self.__gamesToMain.destroy()
        self.__gameSelection.destroy()
        self.__traditional.destroy()
        self.__extreme.destroy()
        self.__blackout.destroy()
        self.__mainMenuButtons()

    #Tradtional to Game Selection
    def __tradToGames(self):
        self.__winsTraditional.destroy()
        self.__anyRow.destroy()
        self.__horizontalBingo.destroy()
        self.__anyColumn.destroy()
        self.__verticalBingo.destroy()
        self.__bothDiagonals.destroy()
        self.__diagonalBingo.destroy()
        self.__playTrad.destroy()
        self.__traditionalToGames.destroy()
        self.__gameTypes()

    #Extreme to Game Selection
    def extremeToGames(self):
        self.__winsExtreme.destroy()
        self.__postCardBingo.destroy()
        self.__playExtreme.destroy()
        self.__extremeToGames.destroy()
        self.__gameTypes()

    #Blackout to Game Selection
    def blkoutToGames(self):
        self.__winsBkout.destroy()
        self.__blackoutBingo.destroy()
        self.__playBkout.destroy()
        self.__blackoutToGames.destroy()
        self.__gameTypes()
        
                            ## PLAY TRADITIONAL ##
    def __playTraditional(self):
        self.__gameSelection.destroy()
        self.__traditional.destroy()
        self.__extreme.destroy()
        self.__blackout.destroy()
        self.__gamesToMain.destroy()
        #title
        self.__winsTraditional = tkinter.Label(self.__topFrame, \
                                               text = "Winning Boards", \
                                               font = "Broadway 50 bold", \
                                               bg = "white", fg = "red")
        self.__winsTraditional.grid()
        #horizontal bingo pic
        self.__anyRow = tkinter.Label(self.__midFrame, text = "*Any Row*", \
                                      bg = "white", width = 8, height = 1, \
                                      font = "Times 20 bold")
        self.__anyRow.grid(row = 0, column = 0)
        self.__horizontalBingoImage = tkinter.PhotoImage(file = \
                                                         "horizontalbingo.gif")
        self.__horizontalBingo = tkinter.Label(self.__midFrame, \
                                               image = \
                                               self.__horizontalBingoImage)
        self.__horizontalBingo.grid(row = 1, column = 0)
        #vertical bingo pic
        self.__anyColumn = tkinter.Label(self.__midFrame,
                                         text = "*Any Column*",bg = "white", \
                                         width = 12, height = 1, \
                                         font = "Times 20 bold")
        self.__anyColumn.grid(row = 0, column = 1)
        self.__verticalBingoImage = tkinter.PhotoImage(file = \
                                                       "verticalbingo.gif")
        self.__verticalBingo = tkinter.Label(self.__midFrame, \
                                             image = \
                                             self.__verticalBingoImage)
        self.__verticalBingo.grid(row = 1, column = 1, padx = 30)
        #diagonal bingo pic
        self.__bothDiagonals = tkinter.Label(self.__midFrame, \
                                             text = "*Both Diagonals*", \
                                             bg = "white", width = 13, \
                                             height = 1, font = "Times 20 bold")
        self.__bothDiagonals.grid(row = 0, column = 2)
        self.__diagonalBingoImage = tkinter.PhotoImage(file = \
                                                       "diagonalbingo.gif")
        self.__diagonalBingo = tkinter.Label(self.__midFrame, \
                                             image = self.__diagonalBingoImage)
        self.__diagonalBingo.grid(row = 1, column = 2, padx = 5)
        #play button
        self.__playTrad = tkinter.Button(self.__midFrame, text = "Play", \
                                         font = "Times 20 bold", bg = "green",\
                                         width = 12, height = 1, \
                                         command = self.__continueTrad)
        self.__playTrad.grid(pady = 20, column = 1)
        #back button
        self.__traditionalToGames = tkinter.Button(self.__midFrame, \
                                                   text = "Back", \
                                                   font = "Times 20 bold", \
                                                   bg = "red", width = 12, \
                                                   height = 1, \
                                                   command = self.__tradToGames)
        self.__traditionalToGames.grid(pady = 5, column = 1)

                                ## PLAY EXTREME ##
    def playExtreme(self):
        self.__gameSelection.destroy()
        self.__traditional.destroy()
        self.__extreme.destroy()
        self.__blackout.destroy()
        self.__gamesToMain.destroy()
        #title
        self.__winsExtreme = tkinter.Label(self.__topFrame, \
                                       text = "Winning Board", \
                                       font = "Broadway 50 bold", \
                                       bg = "white", fg = "red")
        self.__winsExtreme.grid()
        #postCard board pic
        self.__extImage = tkinter.PhotoImage(file = "postCard.gif")
        self.__postCardBingo = tkinter.Label(self.__midFrame, image = \
                                             self.__extImage)
        self.__postCardBingo.grid(row = 0, column = 1)
        #play button
        self.__playExtreme = tkinter.Button(self.__midFrame, text = "Play",\
                                        font = "Times 20 bold", bg = "green",\
                                        width = 12, height = 1, \
                                        command = self.__continueExt)
        self.__playExtreme.grid(row = 1, column = 1, pady = 20)
        #back button
        self.__extremeToGames = tkinter.Button(self.__midFrame, text = "Back", \
                                             font = "Times 20 bold", bg = "red",\
                                             width = 12, height = 1, \
                                             command = self.extremeToGames)
        self.__extremeToGames.grid(row = 2, column = 1)

                            ## PLAY BLACKOUT ##
    def playBlackout(self):
        self.__gameSelection.destroy()
        self.__traditional.destroy()
        self.__extreme.destroy()
        self.__blackout.destroy()
        self.__gamesToMain.destroy()
        #title
        self.__winsBkout = tkinter.Label(self.__topFrame, \
                                       text = "Winning Board", \
                                       font = "Broadway 50 bold", \
                                       bg = "white", fg = "red")
        self.__winsBkout.grid()
        #blackout winning board
        self.__blackoutImage = tkinter.PhotoImage(file = "blackoutBingo.gif")
        self.__blackoutBingo = tkinter.Label(self.__midFrame, image = \
                                             self.__blackoutImage)
        self.__blackoutBingo.grid(row = 0, column = 1)
        #play button
        self.__playBkout = tkinter.Button(self.__midFrame, text = "Play",\
                                           font = "Times 20 bold", \
                                           bg = "green", width = 12, \
                                           height = 1, \
                                           command = self.__continueBkout)
        self.__playBkout.grid(row = 2, column = 1, pady = 20)
        #back button
        self.__blackoutToGames = tkinter.Button(self.__midFrame, text = "Back", \
                                          font = "Times 20 bold", bg = "red",\
                                          width = 12, height = 1,
                                          command = self.blkoutToGames)
        self.__blackoutToGames.grid(row = 3, column = 1)
        
    #Quit Button
    def __quitGame(self):
        option = tkinter.messagebox.askyesno(title = "Quit", \
                                             message = "Do you really" +\
                                             " want to Quit?", \
                                             parent = self.__homeScreen)
        if option == True:
            self.__homeScreen.destroy()
            
MainMenu()

        
        
        

        
