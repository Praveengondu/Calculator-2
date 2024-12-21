import tkinter as tk
from tkinter import messagebox

def press(key):
    current = entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, current + key)

def clear():
    entry.delete(0, tk.END)

def calculate():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, str(result))
    except Exception as e:
        messagebox.showerror("Error", "Invalid Input")

# Create the main window
root = tk.Tk()
root.title("Simple Calculator")

# Entry widget for the input
entry = tk.Entry(root, width=20, font=('Arial', 18), bd=5, insertwidth=4, justify='right')
entry.grid(row=0, column=0, columnspan=4)

# Button layout
buttons = [
    ('7', 1, 0), ('8', 1, 1), ('9', 1, 2), ('/', 1, 3),
    ('4', 2, 0), ('5', 2, 1), ('6', 2, 2), ('*', 2, 3),
    ('1', 3, 0), ('2', 3, 1), ('3', 3, 2), ('-', 3, 3),
    ('C', 4, 0), ('0', 4, 1), ('=', 4, 2), ('+', 4, 3),
]

# Add buttons to the grid
for (text, row, col) in buttons:
    if text == "=":
        button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18), command=calculate)
    elif text == "C":
        button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18), command=clear)
    else:
        button = tk.Button(root, text=text, padx=20, pady=20, font=('Arial', 18),
                           command=lambda key=text: press(key))
    button.grid(row=row, column=col, sticky='nsew')

# Adjust row and column sizes
for i in range(5):
    root.grid_rowconfigure(i, weight=1)
    root.grid_columnconfigure(i, weight=1)

# Run the application
root.mainloop()
