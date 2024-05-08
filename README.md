import tkinter as tk
from tkinter import messagebox
import random
import string

def generate_password():
    length = length_var.get()
    use_uppercase = uppercase_var.get()
    use_lowercase = lowercase_var.get()
    use_numbers = numbers_var.get()
    use_special_chars = special_chars_var.get()

    chars = []
    if use_uppercase:
        chars.extend(string.ascii_uppercase)
    if use_lowercase:
        chars.extend(string.ascii_lowercase)
    if use_numbers:
        chars.extend(string.digits)
    if use_special_chars:
        chars.extend(string.punctuation)

    if not chars:
        messagebox.showerror("Error", "Please select at least one character type.")
        return

    password = ''.join(random.choice(chars) for _ in range(length))
    password_var.set(password)

# Create the main window
root = tk.Tk()
root.title("Password Generator")

# Create variables for checkboxes and password length
length_var = tk.IntVar(value=12)
uppercase_var = tk.BooleanVar(value=True)
lowercase_var = tk.BooleanVar(value=True)
numbers_var = tk.BooleanVar(value=True)
special_chars_var = tk.BooleanVar(value=True)
password_var = tk.StringVar()

# Create widgets
length_label = tk.Label(root, bg='orange', fg="black",text="Password Length:")
length_entry = tk.Entry(root, textvariable=length_var, width=5)
uppercase_check = tk.Checkbutton(root,bg='yellow', fg="black", text="Uppercase", variable=uppercase_var)
lowercase_check = tk.Checkbutton(root, bg='yellow', fg="black",text="Lowercase", variable=lowercase_var)
numbers_check = tk.Checkbutton(root,bg='yellow', fg="black", text="Numbers", variable=numbers_var)
special_chars_check = tk.Checkbutton(root,bg='yellow', fg="black", text="Special Characters", variable=special_chars_var)
generate_button = tk.Button(root,bg='red', fg="white", text="Generate Password", command=generate_password)
password_label = tk.Label(root,bg='aqua', fg="black", text="Generated Password:")
password_entry = tk.Entry(root, textvariable=password_var, state="readonly", width=30)

# Grid layout
length_label.grid(row=0, column=0, padx=5, pady=5, sticky="w")
length_entry.grid(row=0, column=1, padx=5, pady=5)
uppercase_check.grid(row=1, column=0, padx=5, pady=5, sticky="w")
lowercase_check.grid(row=2, column=0, padx=5, pady=5, sticky="w")
numbers_check.grid(row=3, column=0, padx=5, pady=5, sticky="w")
special_chars_check.grid(row=4, column=0, padx=5, pady=5, sticky="w")
generate_button.grid(row=5, column=0, columnspan=2, padx=5, pady=5)
password_label.grid(row=6, column=0, padx=5, pady=5, sticky="w")
password_entry.grid(row=6, column=1, padx=5, pady=5)
root.configure(bg="grey")

# Start the GUI
root.mainloop()
