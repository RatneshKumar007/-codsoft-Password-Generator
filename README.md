# -codsoft-Password-Generator
import tkinter as tk
from tkinter import messagebox
import random
import string

# Function to generate password
def generate_password():
    try:
        length = int(length_entry.get())
        if length <= 0:
            raise ValueError

        characters = string.ascii_lowercase
        if uppercase_var.get():
            characters += string.ascii_uppercase
        if numbers_var.get():
            characters += string.digits
        if symbols_var.get():
            characters += string.punctuation

        if not characters:
            messagebox.showwarning("Input Error", "Please select at least one character type.")
            return

        password = ''.join(random.choice(characters) for _ in range(length))
        result_entry.delete(0, tk.END)
        result_entry.insert(0, password)

    except ValueError:
        messagebox.showwarning("Input Error", "Please enter a valid number.")

# Function to copy password to clipboard
def copy_password():
    password = result_entry.get()
    root.clipboard_clear()
    root.clipboard_append(password)
    messagebox.showinfo("Copied", "Password copied to clipboard!")

# GUI window setup
root = tk.Tk()
root.title("Password Generator")
root.geometry("400x400")
root.config(bg="#f7f7f7")

# Title
tk.Label(root, text="🔐 Password Generator", font=("Helvetica", 18, "bold"), bg="#f7f7f7").pack(pady=10)

# Password Length
tk.Label(root, text="Password Length:", font=("Helvetica", 12), bg="#f7f7f7").pack()
length_entry = tk.Entry(root, font=("Helvetica", 12), justify="center")
length_entry.pack(pady=5)

# Options
uppercase_var = tk.BooleanVar()
numbers_var = tk.BooleanVar()
symbols_var = tk.BooleanVar()

tk.Checkbutton(root, text="Include Uppercase", variable=uppercase_var, bg="#f7f7f7").pack()
tk.Checkbutton(root, text="Include Numbers", variable=numbers_var, bg="#f7f7f7").pack()
tk.Checkbutton(root, text="Include Symbols", variable=symbols_var, bg="#f7f7f7").pack()

# Generate Button
tk.Button(root, text="Generate Password", font=("Helvetica", 12), command=generate_password).pack(pady=15)

# Output field
result_entry = tk.Entry(root, font=("Helvetica", 14), justify="center")
result_entry.pack(pady=10, padx=20, fill=tk.X)

# Copy Button
tk.Button(root, text="Copy to Clipboard", font=("Helvetica", 12), command=copy_password).pack(pady=10)

# Start the app
root.mainloop()
