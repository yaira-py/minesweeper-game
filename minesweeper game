import tkinter as tk
import random
from tkinter import messagebox


class MineSweeper:
    def __init__(self,root):
        self.root=root
        self.root.title('MineSweeper')
        self.root.configure(bg="#f0f0f0")

        self.rows=9
        self.cols=9
        self.mines=10
        self.buttons={}

        self.mine_position=set()
        self.revealed=set()
        self.game_over=False

        tk.Label(self.root,text='MineSweaper 💥',font=('Arial',16,'bold'),bg='#f0f0f0').pack(pady=10)

        self.frame=tk.Frame(self.root,bg='#f0f0f0')
        self.frame.pack(pady=5)

        self.setup_game()
        tk.Button(self.root,text='New Game',font=('Arial',11,'bold'),bg='yellow',command=self.restart).pack(pady=10)


    def setup_game(self):
        all_cells=[(r,c) for r in range(self.rows) for c in range(self.cols)]
        self.mine_position=set(random.sample(all_cells,self.mines))

        for r in range(self.rows):
            for c in range(self.cols):
                btn= tk.Button(self.frame,width=3,height=1,font=('Arial',12,'bold'),command=lambda r=r, c=c: self.click(r,c))
                btn.grid(row=r,column=c)

                btn.bind('<Button-3>', lambda e, r=r,c=c: self.flag(r,c))
                self.buttons[(r,c)]=btn


    def count_nearby_mines(self,r,c):
        count=0
        for dr in [-1,0,1]:
            for dc in [-1,0,1]:
                nr,nc,=r+dr,c+dc
                if (nr,nc) in self.mine_position:
                    count+=1
        return count


    def click(self,r,c):
        if self.game_over or (r,c) in self.revealed:
            return

        btn=self.buttons[(r,c)]

        if (r,c) in self.mine_position:
            btn.config(text='💣',bg='red')
            self.show_all_mines()
            self.game_over=True
            messagebox.showinfo('Game over','Bomb blasted 💥')
            return

        mines_near=self.count_nearby_mines(r,c)
        self.revealed.add((r,c))
        btn.config(text=str(mines_near) if mines_near>0 else '', bg="lightgrey",state='disabled')

        if mines_near==0:
            for dr in [-1,0,1]:
                for dc in [-1,0,1]:
                    nr,nc=r+dr,c+dc
                    if 0<=nr< self.rows and 0<= nc < self.cols:
                        self.click(nr,nc)

        if len(self.revealed)==(self.rows*self.cols-self.mines):
            self.game_over=True
            messagebox.showinfo('You win!','you won the game')


    def flag(self,r,c):
        if self.game_over or (r,c) in self.revealed:
            return
        btn=self.buttons[(r,c)]

        if btn.cget('text')=='🚩':
            btn.config(text='')

        else:
            btn.config(text='🚩')

    def show_all_mines(self):
        for pos in self.mine_position:
            self.buttons[pos].config(text='💣',bg='#ffcccc')


    def restart(self):
        for btn in self.buttons.values():
            btn.destroy()

        self.buttons={}
        self.revealed=set()
        self.game_over=False
        self.setup_game()

        





if __name__=="__main__":
    win=tk.Tk()
    app=MineSweeper(win)
    win.mainloop()
