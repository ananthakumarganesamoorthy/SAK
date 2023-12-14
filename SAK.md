import tkinter as tk
from tkinter import ttk, messagebox

def validate_login():
    # Replace these with your actual username and password
    correct_username = "SAK"
    correct_password = "12345"

    entered_username = username_entry.get()
    entered_password = password_entry.get()

    if entered_username == correct_username and entered_password == correct_password:
        open_dashboard()
    else:
        messagebox.showerror("Login Failed", "Invalid username or password")

def open_dashboard():
    # Destroy the login window
    root.destroy()

    # Create a new window for the dashboard
    dashboard_window = tk.Tk()
    dashboard_window.title("Street Light Control Dashboard")

    # Add widgets for options
    ttk.Label(dashboard_window, text="Choose Option:").pack(pady=10)
    option_var = tk.StringVar()
    option_var.set("Light Intensity")  # Default option
    options_menu = ttk.Combobox(dashboard_window, values=["Light Intensity", "Light Status", "Usage of Light"], textvariable=option_var)
    options_menu.pack(pady=10)

    # Validate and perform actions based on the selected option
    def submit_option():
        selected_option = option_var.get()
        if selected_option == "Light Intensity":
            messagebox.showinfo("Option Selected", "Displaying Light Intensity information.")
            # Implement actions for Light Intensity option here
        elif selected_option == "Light Status":
            messagebox.showinfo("Option Selected", "Displaying Light Status information.")
            # Implement actions for Light Status option here
        elif selected_option == "Usage of Light":
            usage_value = light_usage_entry.get()
            if not usage_value:
                messagebox.showerror("Validation Error", "Please enter a value for light usage.")
            else:
                try:
                    float(usage_value)  # Check if it's a valid number
                    messagebox.showinfo("Submission Successful", "Light usage submitted successfully!")
                    # Implement actions for Usage of Light option here
                except ValueError:
                    messagebox.showerror("Validation Error", "Please enter a valid number for light usage.")
        else:
            messagebox.showerror("Option Error", "Invalid option selected.")

    # Back button to return to the login page
    back_button = ttk.Button(dashboard_window, text="Back to Login", command=lambda: back_to_login(dashboard_window))
    back_button.pack(pady=20)

    # Submit button to validate the selected option and perform actions
    submit_button = ttk.Button(dashboard_window, text="Submit", command=submit_option)
    submit_button.pack(pady=10)

    # Start the Tkinter main loop for the dashboard window
    dashboard_window.mainloop()

def back_to_login(dashboard_window):
    # Close the dashboard window and recreate the login window
    dashboard_window.destroy()
    create_login_window()

def create_login_window():
    # Create the main window
    global root
    root = tk.Tk()
    root.title("Street Light Control System Login")

    # Use the 'ttkthemes' library to create a themed interface
    style = ttk.Style()
    style.theme_use('clam')  # You can experiment with different themes (aqua, classic, vista, winnative, clam, ...)

    # Create and place widgets with a more sophisticated design
    frame = ttk.Frame(root, padding="10")
    frame.grid(row=0, column=0, sticky=(tk.W, tk.E, tk.N, tk.S))

    ttk.Label(frame, text="Username:").grid(row=0, column=0, pady=10)
    global username_entry
    username_entry = ttk.Entry(frame)
    username_entry.grid(row=0, column=1, pady=10)

    ttk.Label(frame, text="Password:").grid(row=1, column=0, pady=10)
    global password_entry
    password_entry = ttk.Entry(frame, show="*")
    password_entry.grid(row=1, column=1, pady=10)

    login_button = ttk.Button(frame, text="Login", command=validate_login)
    login_button.grid(row=2, column=0, columnspan=2, pady=20)

    # Start the Tkinter main loop for the login window
    root.mainloop()

# Start the initial login window
create_login_window()
