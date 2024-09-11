import tkinter as tk
from tkinter import messagebox
import re

def main():
    try:
        # Create main application window
        root = tk.Tk()
        root.title("Login & Register")
        root.geometry("389x317")
        root.configure(bg="#272930")

        # Remove title bar, including minimize and maximize buttons
        root.overrideredirect(True)
        root.resizable(False, False)

        # Color scheme
        bg_color = "#272930"
        entry_bg = "#313645"
        entry_fg = "#c2c6dc"
        text_color = "#c2c6dc"
        button_color = "#3c3e4f"
        button_active_color = "#4e5366"
        button_fg_color = "white"
        toolbar_color = "#1f2430"
        check_fg_color = "#c2c6dc"

        # Function to handle window dragging
        def on_drag(event):
            x = root.winfo_pointerx() - x_offset
            y = root.winfo_pointery() - y_offset
            root.geometry(f"+{x}+{y}")

        def on_press(event):
            global x_offset, y_offset
            x_offset = root.winfo_pointerx() - root.winfo_rootx()
            y_offset = root.winfo_pointery() - root.winfo_rooty()

        root.bind("<Button-1>", on_press)
        root.bind("<B1-Motion>", on_drag)

        # Function to close the window
        def close_window():
            root.destroy()

        # Create a small custom toolbar with just a close button
        toolbar = tk.Frame(root, bg=toolbar_color, height=20, relief='flat', bd=0)
        toolbar.pack(fill='x', side='top')

        # Close button on the toolbar
        close_button = tk.Button(toolbar, text="X", command=close_window, bg=toolbar_color, fg=button_fg_color, activebackground=button_active_color, relief='flat', padx=5, pady=2)
        close_button.pack(side='right')

        # Function to switch to the register window
        def show_register():
            login_frame.pack_forget()
            register_frame.pack()

        # Function to switch back to the login window
        def show_login():
            register_frame.pack_forget()
            login_frame.pack()

        # Function to validate email format using regex
        def is_valid_email(email):
            pattern = r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$'
            return re.match(pattern, email)

        # Function for register action
        def register():
            username = reg_username_entry.get()
            password = reg_password_entry.get()
            repeat_password = reg_repeat_password_entry.get()
            email = reg_email_entry.get()

            if password != repeat_password:
                messagebox.showerror("Register", "Passwords do not match")
                return

            if not is_valid_email(email):
                messagebox.showerror("Register", "Invalid email format")
                return

            messagebox.showinfo("Register", "Registration Successful!")
            show_login()

        # Function for login action
        def login():
            username = login_username_entry.get()
            password = login_password_entry.get()
            if username == "jacobsins11" and password == "password123":
                messagebox.showinfo("Login", "Login Successful!")
            else:
                messagebox.showerror("Login", "Incorrect Username or Password")

        # ----------- Login Frame ------------
        login_frame = tk.Frame(root, bg=bg_color, padx=20, pady=20)

        # Username Entry
        login_username_entry = tk.Entry(login_frame, bg=entry_bg, fg=entry_fg, insertbackground=entry_fg, relief='flat', width=30, highlightthickness=1, highlightbackground="#454b5e")
        login_username_entry.pack(pady=5, ipady=5)

        # Password Entry
        login_password_entry = tk.Entry(login_frame, show="*", bg=entry_bg, fg=entry_fg, insertbackground=entry_fg, relief='flat', width=30, highlightthickness=1, highlightbackground="#454b5e")
        login_password_entry.pack(pady=5, ipady=5)

        # Remember Me Checkbox
        remember_var = tk.IntVar()
        remember_check = tk.Checkbutton(login_frame, text="Remember Me", variable=remember_var, bg=bg_color, fg=check_fg_color, activebackground=bg_color, selectcolor=entry_bg, anchor='w')
        remember_check.pack(pady=5)

        # Buttons for Login and Register
        button_frame = tk.Frame(login_frame, bg=bg_color)
        button_frame.pack(pady=10)

        login_button = tk.Button(button_frame, text="Login", command=login, bg=button_color, fg=button_fg_color, activebackground=button_active_color, relief='flat', padx=20, pady=5)
        login_button.grid(row=0, column=0, padx=5)

        register_button = tk.Button(button_frame, text="Register", command=show_register, bg=button_color, fg=button_fg_color, activebackground=button_active_color, relief='flat', padx=20, pady=5)
        register_button.grid(row=0, column=1, padx=5)

        login_frame.pack()

        # ----------- Register Frame (Smaller) ------------
        register_frame = tk.Frame(root, bg=bg_color, padx=10, pady=10)

        inner_register_frame = tk.Frame(register_frame, bg=bg_color)  # Inner frame for smaller size
        inner_register_frame.pack()

        tk.Label(inner_register_frame, text="Username", bg=bg_color, fg=text_color).pack(pady=2)
        reg_username_entry = tk.Entry(inner_register_frame, bg=entry_bg, fg=text_color, insertbackground=text_color, relief='flat', width=25, highlightthickness=1, highlightbackground="#454b5e")
        reg_username_entry.pack(pady=2, ipady=3)

        tk.Label(inner_register_frame, text="Password", bg=bg_color, fg=text_color).pack(pady=2)
        reg_password_entry = tk.Entry(inner_register_frame, show="*", bg=entry_bg, fg=text_color, insertbackground=text_color, relief='flat', width=25, highlightthickness=1, highlightbackground="#454b5e")
        reg_password_entry.pack(pady=2, ipady=3)

        tk.Label(inner_register_frame, text="Repeat Password", bg=bg_color, fg=text_color).pack(pady=2)
        reg_repeat_password_entry = tk.Entry(inner_register_frame, show="*", bg=entry_bg, fg=text_color, insertbackground=text_color, relief='flat', width=25, highlightthickness=1, highlightbackground="#454b5e")
        reg_repeat_password_entry.pack(pady=2, ipady=3)

        tk.Label(inner_register_frame, text="Email", bg=bg_color, fg=text_color).pack(pady=2)
        reg_email_entry = tk.Entry(inner_register_frame, bg=entry_bg, fg=text_color, insertbackground=text_color, relief='flat', width=25, highlightthickness=1, highlightbackground="#454b5e")
        reg_email_entry.pack(pady=2, ipady=3)

        # Buttons for Register and Cancel
        reg_button_frame = tk.Frame(inner_register_frame, bg=bg_color)
        reg_button_frame.pack(pady=5)

        register_btn = tk.Button(reg_button_frame, text="Register", command=register, bg=button_color, fg=button_fg_color, activebackground=button_active_color, relief='flat', padx=15, pady=3)
        register_btn.grid(row=0, column=0, padx=5)

        cancel_btn = tk.Button(reg_button_frame, text="Cancel", command=show_login, bg=button_color, fg=button_fg_color, activebackground=button_active_color, relief='flat', padx=15, pady=3)
        cancel_btn.grid(row=0, column=1, padx=5)

        # Initially show the login frame
        login_frame.pack()

        root.mainloop()
    except Exception as e:
        print(f"An error occurred: {e}")
        messagebox.showerror("Error", str(e))

if __name__ == "__main__":
    main()
