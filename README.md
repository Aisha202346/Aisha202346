import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk  # For handling the image

#Function to calculate total marks
def calculate_total():
    try:
        marks = [int(subject.get()) for subject in [sub1, sub2, sub3, sub4, sub5]]
        total_marks = sum(marks)
        total_label.config(text=f"Total Marks: {total_marks}")
    except ValueError:
        messagebox.showerror("Input Error", "Please enter valid integer marks for all subjects.")

# Function to calculate percentage
def calculate_percentage():
    try:
        marks = [int(subject.get()) for subject in [sub1, sub2, sub3, sub4, sub5]]
        total_marks = sum(marks)
        percentage = (total_marks / 500) * 100
        percentage_label.config(text=f"Percentage: {percentage:.2f}%")
    except ValueError:
        messagebox.showerror("Input Error", "Please enter valid integer marks for all subjects.")

# Main application window
root = tk.Tk()
root.title("Student Marks and Percentage Calculator")
root.geometry("500x500")
root.config(bg="#f0f8ff")  # Light blue background

# Add MUET logo
try:
    logo_image = Image.open("muet_logo.png")
    logo_image = logo_image.resize((150, 150), Image.ANTIALIAS)
    logo = ImageTk.PhotoImage(logo_image)
    logo_label = tk.Label(root, image=logo, bg="#f0f8ff")
    logo_label.pack(pady=10)
except Exception:
    messagebox.showwarning("Image Error", "MUET logo not found. Please add 'muet_logo.png' in the working directory.")

# Title label
title_label = tk.Label(root, text="MUET Student Marks Calculator", font=("Arial", 16, "bold"), bg="#f0f8ff", fg="#003366")
title_label.pack(pady=10)

# Subject entry fields
sub1 = tk.StringVar()
sub2 = tk.StringVar()
sub3 = tk.StringVar()
sub4 = tk.StringVar()
sub5 = tk.StringVar()

fields = [
    ("Subject 1 Marks:", sub1),
    ("Subject 2 Marks:", sub2),
    ("Subject 3 Marks:", sub3),
    ("Subject 4 Marks:", sub4),
    ("Subject 5 Marks:", sub5),
]

for text, var in fields:
    frame = tk.Frame(root, bg="#f0f8ff")
    frame.pack(pady=5)
    label = tk.Label(frame, text=text, font=("Arial", 12), bg="#f0f8ff", fg="#003366")
    label.pack(side="left", padx=5)
    entry = tk.Entry(frame, textvariable=var, font=("Arial", 12), width=10)
    entry.pack(side="left", padx=5)

# Buttons to calculate total and percentage
button_frame = tk.Frame(root, bg="#f0f8ff")
button_frame.pack(pady=20)

total_button = tk.Button(button_frame, text="Calculate Total Marks", font=("Arial", 12, "bold"), bg="#003366", fg="#ffffff", command=calculate_total)
total_button.grid(row=0, column=0, padx=10)

percentage_button = tk.Button(button_frame, text="Calculate Percentage", font=("Arial", 12, "bold"), bg="#003366", fg="#ffffff", command=calculate_percentage)
percentage_button.grid(row=0, column=1, padx=10)

# Labels to display results
total_label = tk.Label(root, text="Total Marks: ", font=("Arial", 14), bg="#f0f8ff", fg="#003366")
total_label.pack(pady=5)

percentage_label = tk.Label(root, text="Percentage: ", font=("Arial", 14), bg="#f0f8ff", fg="#003366")
percentage_label.pack(pady=5)

# Run the application
root.mainloop()

