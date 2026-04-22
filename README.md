# -queue-managment-software-
import tkinter as tk
from tkinter import messagebox

# Queue storage
queue = []
current_serving = "None"

# Functions
def join_queue():
    name = entry_name.get().strip()
    
    if name == "":
        messagebox.showwarning("Input Error", "Please enter a name")
        return
    
    queue.append(name)
    entry_name.delete(0, tk.END)
    update_display()

def serve_next():
    global current_serving
    
    if not queue:
        messagebox.showinfo("Queue Empty", "No customers in queue")
        return
    
    current_serving = queue.pop(0)
    label_serving.config(text=f"Now Serving: {current_serving}")
    update_display()

def clear_queue():
    global queue, current_serving
    queue.clear()
    current_serving = "None"
    label_serving.config(text="Now Serving: None")
    update_display()

def update_display():
    listbox.delete(0, tk.END)
    
    if not queue:
        listbox.insert(tk.END, "Queue is empty")
    else:
        for i, name in enumerate(queue, start=1):
            listbox.insert(tk.END, f"{i}. {name}")

# Main Window
root = tk.Tk()
root.title("Queue Management System")
root.geometry("450x500")
root.resizable(False, False)

# Title
title = tk.Label(root, text="Queue Management System", font=("Arial", 16, "bold"))
title.pack(pady=10)

# Input
entry_name = tk.Entry(root, width=30, font=("Arial", 12))
entry_name.pack(pady=10)

# Buttons
btn_join = tk.Button(root, text="Join Queue", width=20, command=join_queue)
btn_join.pack(pady=5)

btn_serve = tk.Button(root, text="Serve Next", width=20, command=serve_next)
btn_serve.pack(pady=5)

btn_clear = tk.Button(root, text="Clear Queue", width=20, command=clear_queue)
btn_clear.pack(pady=5)

# Now Serving Label
label_serving = tk.Label(root, text="Now Serving: None", font=("Arial", 12))
label_serving.pack(pady=15)

# Queue List
listbox = tk.Listbox(root, width=40, height=10, font=("Arial", 11))
listbox.pack(pady=10)

# Run application
root.mainloop()
