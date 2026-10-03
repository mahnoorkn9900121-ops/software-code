import tkinter as tk
from tkinter import messagebox
import webbrowser


def open_tabs(event=None):
    website = website_entry.get().strip()
    number_text = number_entry.get().strip()

    if not website:
        messagebox.showerror("Error", "Website enter karo.")
        return

    if not number_text.isdigit():
        messagebox.showerror("Error", "Number mein sirf digits enter karo.")
        return

    number = int(number_text)

    if number <= 0:
        messagebox.showerror("Error", "Number 1 ya us se zyada hona chahiye.")
        return

    # Agar user ne https:// nahi likha
    if not website.startswith(("http://", "https://")):
        website = "https://" + website

    # Jitni baar number diya hai, utne tabs open honge
    for _ in range(number):
        webbrowser.open_new_tab(website)


# Main window
root = tk.Tk()
root.title("Website Tab Opener")
root.geometry("450x250")
root.resizable(False, False)

# Heading
title = tk.Label(
    root,
    text="Website Tab Opener",
    font=("Arial", 18, "bold")
)
title.pack(pady=20)

# Website
website_label = tk.Label(root, text="Website:")
website_label.pack()

website_entry = tk.Entry(root, width=45)
website_entry.pack(pady=5)

# Number
number_label = tk.Label(root, text="Number of Tabs:")
number_label.pack()

number_entry = tk.Entry(root, width=45)
number_entry.pack(pady=5)

# Button
open_button = tk.Button(
    root,
    text="Open Tabs",
    command=open_tabs,
    width=20
)
open_button.pack(pady=15)

# Enter key se bhi tabs open hon
root.bind("<Return>", open_tabs)

# Software start
root.mainloop()
