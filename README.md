import tkinter as tk

def click_button(char):
    current_text = result_display.get()
    if current_text == "Error":
        current_text = ""
    result_display.set(current_text + char)

def clear():
    result_display.set("")

def calculate():
    try:
        expression = result_display.get()
        result = eval(expression)
        result_display.set(result)
    except Exception as e:
        result_display.set("Error")

# Create a tkinter window
root = tk.Tk()
root.title("Calculator")

# Result display
result_display = tk.StringVar()
result_display.set("")

result_label = tk.Label(root, textvariable=result_display, font=("Arial", 20), bd=10, bg="lightgray", anchor="e")
result_label.grid(row=0, column=0, columnspan=4)

# Calculator buttons
button_text = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    'C', '0', '=', '+'
]

row_val = 1
col_val = 0

for char in button_text:
    if char == 'C':
        button = tk.Button(root, text=char, padx=20, pady=20, font=("Arial", 16), bg="red", fg="white", command=clear)
    elif char == '=':
        button = tk.Button(root, text=char, padx=20, pady=20, font=("Arial", 16), bg="green", fg="white", command=calculate)
    else:
        button = tk.Button(root, text=char, padx=20, pady=20, font=("Arial", 16), command=lambda char=char: click_button(char))
    button.grid(row=row_val, column=col_val)
    col_val += 1
    if col_val > 3:
        col_val = 0
        row_val += 1

# Run the tkinter main loop
root.mainloop()
