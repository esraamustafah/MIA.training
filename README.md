# MIA.training
import tkinter as tk
import random
file_path = r"C:\Users\B-ONE\Desktop\c++\Dr Frank\.vscode\words.txt"
with open(file_path , "r") as f :
    words = [w.strip().lower() for w in f if len(w.strip()) ==5]
secret = random.choice(words)    
print ("just trying " , secret)
#preparing the main window
root = tk.Tk()
root.title("Wordle Game")
root.geometry("400x500")
root.resizable(False,False)
#preparing the game grid
rows , cols =  6,5
labels = [[None for _ in range (cols)] for _ in range (rows)]
current_row=0 #following the line the player plays it 
#grid colors
colors = {
    "green" : "#6aaa64" ,
    "yellow" : "#c9b458" ,
    "gray" : "#787c7e" }
#building the interface
for r in range(rows) :
    for c in range (cols) :
        label_box = tk.Label (root , text ="" , width = 4 , height =2 , font = ("Helvetica" , 18 , "bold") , relief = "solid" , borderwidth =1 , bg = "white")
        label_box.grid(row = r , column = c , padx=5 , pady=6)
        labels [r] [c] = label_box
#function for detecting
def check_word () :
    global current_row
    guess = entry.get().lower()
    if len(guess) != 5 :
        status.config(text ="Word must be 5 letters" , fg="red")
        return
    if guess not in words :
        status.config(text = "word is not in list" , fg="red")
        return 
    for i in range(cols) :
        labels [current_row] [i].config(text=guess[i].upper())
        if guess[i] == secret[i] :
            labels[current_row][i].config(bg = colors["green"] , fg="white")    
        elif guess[i] in secret :
            labels[current_row][i].config(bg = colors["yellow"] , fg = "white")
        else :
            labels[current_row][i].config(bg=colors["gray"] , fg="white")
    if guess == secret :
        status.config(text= "YOU HAD WON!!", fg="green")
        entry.config(state = "disabled")
    else :
        current_row += 1 
        if current_row == rows :
            status.config(text = f"game over , the secret word was :  {secret.upper()} ", fg="red" )
            entry.config(state= "disabled")
            return
    entry.delete(0 , tk.END)   
entry=tk.Entry(root , font= ("helvetica" , 18), justify="center") 
entry.grid(row=rows , column=0 , columnspan=3 , pady=10)
btn = tk.Button(root , text="GUESS?", font=("helvetica" , 14) , command = check_word)
btn.grid(row = rows , column=3 , columnspan=2)
status = tk.Label(root , text = "" , font =("helvetica", 12) )
status.grid (row = rows+1 , column=0 , columnspan=5)
root.mainloop()
            
status = tk.Label(root , text = "" , font =("helvetica", 12) )
status.grid (row = rows+1 , column=0 , columnspan=5)
root.mainloop()
