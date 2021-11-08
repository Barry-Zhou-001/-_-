import numpy as np
import tkinter as tk
from tkinter import filedialog
from tkinter import *
import tkinter.messagebox

#判断输入序列是否正常
def isnormal(seq):
    num_A = seq.count("A")
    num_T = seq.count("T")
    num_C = seq.count("C")
    num_G = seq.count("G")
    return num_A + num_T + num_C + num_G == len(seq)

#构建反向互补函数
def Reverse_Complementarity(seq):
    intab = 'ATCG'
    outtab = "TAGC"
    trantab = str.maketrans(intab,outtab)
    seq_complentarity = seq.translate(trantab)  ##使用string的translate函数将序列变为互补
    seq_list = list(seq_complentarity)
    seq_list.reverse()  ##使用list的reverse函数将序列反向
    seq_out = "".join(seq_list)
    return seq_out

#获取文件路径
def getLocalFile():
    root=tk.Tk()
    root.withdraw()
    filePath=filedialog.askopenfilename()
    #print('文件路径：',filePath)
    return filePath

#读取文件
def read_fasta(filePath): #用def定义函数read_fasta()，并向函数传递参数用变量input接收
    with open(filePath,'r') as f: # 打开文件
        fasta = {} # 定义一个空的字典
        for line in f:
            line = line.strip() # 去除末尾换行符
            if line[0] == '>':
                header = line[1:]
            else:
                sequence = line
                fasta[header] = fasta.get(header,'') + sequence
    return fasta

#序列互补功能封装
def Function(seq):
    if isnormal(seq):
        result = Reverse_Complementarity(seq)
        root1 = tk.Tk()
        root1.title("Reverse_Complementarity")
        text = tk.Text(root1,width=50,height=40)
        text.insert(tk.INSERT,"原始序列：\n")
        text.insert(tk.INSERT,'%s'%seq)
        text.insert(tk.INSERT,"\n\n反向互补序列：\n")
        text.insert(tk.INSERT,'%s'%result)
        text.pack()
    else:
        tkinter.messagebox.showinfo('提示','序列含ATCG之外字符')

#本地文件查询
def F1():
    filePath = getLocalFile()
    fasta_dict = read_fasta(filePath)
    seq = ''.join(fasta_dict.values())
    Function(seq)

#输入序列查询
def F2():
    seq = entry1.get("1.0",END)
    seq = seq.strip()
    Function(seq)
    
if __name__ == '__main__':
    root = tk.Tk()
    root.title("求反向互补序列")
    root.geometry('450x400')
    
    label1 = tk.Label(text="Sequence", width=50, height=2)
    label1.pack()
    entry1 = tk.Text(root, width=60 , height=22)
    entry1.pack()

    button1 = tk.Button(text="本地文件查询" ,width=15, height=2, command=F1)
    button1.pack(padx=40, pady=10, side="left")
    button2 = tk.Button(text="输入序列查询" ,width=15, height=2, command=F2)
    button2.pack(padx=35, pady=10, side="left")

    root.mainloop()
