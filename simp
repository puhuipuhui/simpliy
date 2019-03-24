# -*- coding:utf-8 -*-
#! python2
from tkinter import *

class Application(Frame):
 def __init__(self):
  Frame.__init__(self)
  self.grid()
  self.mem = ''    # 内存中的数据
  self.opt = ''    # 操作符
  self.display = StringVar() # 显示的数据
  self.display.set('0')  # 初始值
  self.need_cls = False  # 是否需要清屏
  self.create_widgets()
 # 清空
 def clear(self):
  self.mem = ''
  self.display.set('0')
 # 取反
 def negative(self):
  self.display.set(eval('-' + self.display.get()))
 # 四则运算
 def option(self, opt):
  if not self.need_cls:
   self.calculate()
  self.opt = opt
  self.need_cls = True
  self.mem = self.display.get()
 # 计算结果
 def calculate(self):
  if self.opt:
   try:
    self.display.set(eval(self.mem + self.opt + self.display.get()))
   except Exception:
    self.display.set('错误')
    self.need_cls = True
   self.opt = ''
   self.mem = ''
 # 百分比
 def percent(self):
  base = float(self.mem or 1) / 100
  display = eval('{}*{}'.format(self.display.get(), base))
  int_display = int(display)
  display = int_display if display == int_display else display
  self.display.set(display)
  self.need_cls = True
 # 输入
 def input(self, key):
  if self.need_cls:
   self.display.set('0')
   self.need_cls = False
  display = self.display.get()
  if display == '0' and key != '.':
   self.display.set(key)
  else:
   if '.' in display and key == '.':
    return
   self.display.set(display + key)
 # 创建组件
 def create_widgets(self):
  # 显示框
  Entry(self, textvariable=self.display, state="readonly", width=35).grid(
   row=0, column=0, columnspan=4)
  # 键盘
  keyboards = [
   ['C', '+/-', '%', '/'], 
   ['7', '8', '9', '*'], 
   ['4', '5', '6', '-'],
   ['1', '2', '3', '+'],
   ['0', '.', '=']
  ]
  for row, keys in enumerate(keyboards):
   row_num = 3 + row
   for col, key in enumerate(keys):
    if key == 'C':
     command = self.clear
    elif key == '+/-':
     command = self.negative
    elif key == '%':
     command = self.percent
    elif key in ['+', '-', '*', '/']:
     command = lambda s=key: self.option(s)
    elif key == '=':
     command = self.calculate
    else:
     command = lambda s=key: self.input(s)
    bt = Button(self, text=key, command=command, width=6)
    bt.grid(row=row_num, column=col)
app = Application()
# 设置窗口标题:
app.master.title(' 计算器')
# 设置窗口尺寸/位置
app.master.geometry("326x170+200+200")
# 设置窗口不可变
app.master.resizable(width=False, height=False)
# 主消息循环:
app.mainloop()
