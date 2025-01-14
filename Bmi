import tkinter as tk
from tkinter import messagebox
import sqlite3
import matplotlib.pyplot as plt
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg

# Create or connect to SQLite database to store user data
conn = sqlite3.connect("bmi_data.db")
cursor = conn.cursor()

# Create table to store user data if it doesn't exist
cursor.execute('''
    CREATE TABLE IF NOT EXISTS bmi_data (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT,
        weight REAL,
        height REAL,
        bmi REAL
    )
''')
conn.commit()

# Function to calculate BMI
def calculate_bmi():
    try:
        weight = float(entry_weight.get())
        height = float(entry_height.get())
        
        # Validate input
        if weight <= 0 or height <= 0:
            raise ValueError("Weight and Height must be positive numbers.")
        
        # Calculate BMI
        bmi = weight / (height ** 2)
        
        # Display BMI result
        label_bmi_result.config(text=f"BMI: {bmi:.2f}")
        
        # Store user data into the database
        name = entry_name.get()
        cursor.execute("INSERT INTO bmi_data (name, weight, height, bmi) VALUES (?, ?, ?, ?)",
                       (name, weight, height, bmi))
        conn.commit()

        messagebox.showinfo("Success", "BMI calculated and saved successfully!")

    except ValueError as e:
        messagebox.showerror("Input Error", str(e))

# Function to display historical BMI data
def view_history():
    cursor.execute("SELECT * FROM bmi_data")
    records = cursor.fetchall()

    if not records:
        messagebox.showinfo("No Data", "No historical data available.")
        return

    history_window = tk.Toplevel(window)
    history_window.title("BMI History")
    history_window.geometry("400x400")

    history_listbox = tk.Listbox(history_window, width=50, height=15)
    history_listbox.pack(pady=10)

    for record in records:
        history_listbox.insert(tk.END, f"Name: {record[1]}, BMI: {record[4]:.2f} (Weight: {record[2]} kg, Height: {record[3]} m)")

# Function to show BMI trends in a graph
def show_bmi_trends():
    cursor.execute("SELECT name, bmi FROM bmi_data")
    records = cursor.fetchall()

    if not records:
        messagebox.showinfo("No Data", "No BMI data available for trend analysis.")
        return

    names = [record[0] for record in records]
    bmis = [record[1] for record in records]

    # Plotting the BMI data
    plt.figure(figsize=(8, 5))
    plt.plot(names, bmis, marker='o', color='b', linestyle='-', markersize=6)
    plt.title("BMI Trend")
    plt.xlabel("Users")
    plt.ylabel("BMI")
    plt.xticks(rotation=45, ha="right")
    plt.tight_layout()
    plt.show()

# Create the main window
window = tk.Tk()
window.title("BMI Calculator")
window.geometry("400x400")

# Add widgets for the user interface
label_name = tk.Label(window, text="Name:")
label_name.pack(pady=5)
entry_name = tk.Entry(window)
entry_name.pack(pady=5)

label_weight = tk.Label(window, text="Weight (kg):")
label_weight.pack(pady=5)
entry_weight = tk.Entry(window)
entry_weight.pack(pady=5)

label_height = tk.Label(window, text="Height (m):")
label_height.pack(pady=5)
entry_height = tk.Entry(window)
entry_height.pack(pady=5)

# Button to calculate BMI
button_calculate = tk.Button(window, text="Calculate BMI", command=calculate_bmi)
button_calculate.pack(pady=10)

# Label to display the BMI result
label_bmi_result = tk.Label(window, text="BMI: N/A", font=("Arial", 14))
label_bmi_result.pack(pady=10)

# Buttons for viewing history and trends
button_history = tk.Button(window, text="View History", command=view_history)
button_history.pack(pady=5)

button_trends = tk.Button(window, text="Show BMI Trends", command=show_bmi_trends)
button_trends.pack(pady=5)

# Run the Tkinter event loop
window.mainloop()

# Close the database connection on exit
conn.close()
