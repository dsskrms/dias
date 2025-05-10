import tkinter as tk
from tkinter import messagebox
import qrcode
from PIL import Image, ImageTk
import os
from io import BytesIO

class QRCodeGenerator:
    def __init__(self, root):
        self.root = root
        self.root.title("QR Code Generator")
        self.root.resizable(True, True)
        
        # Configure grid weights for responsiveness
        for i in range(4):
            self.root.grid_rowconfigure(i, weight=1)
        for i in range(3):
            self.root.grid_columnconfigure(i, weight=1)
        
        # GUI Elements
        tk.Label(root, text="Enter Content:", font=("Helvetica", 12)).grid(row=0, column=0, sticky="e", padx=5, pady=5)
        self.content_var = tk.StringVar()
        tk.Entry(root, textvariable=self.content_var, width=30, font=("Helvetica", 12)).grid(row=0, column=1, sticky="ew", padx=5, pady=5)
        
        tk.Label(root, text="File Name:", font=("Helvetica", 12)).grid(row=1, column=0, sticky="e", padx=5, pady=5)
        self.filename_var = tk.StringVar()
        tk.Entry(root, textvariable=self.filename_var, width=30, font=("Helvetica", 12)).grid(row=1, column=1, sticky="ew", padx=5, pady=5)
        
        tk.Button(root, text="Generate QR", command=self.generate_qr, width=15, font=("Helvetica", 12)).grid(row=0, column=2, sticky="ew", padx=5, pady=5)
        tk.Button(root, text="Save QR", command=self.save_qr, width=15, font=("Helvetica", 12)).grid(row=1, column=2, sticky="ew", padx=5, pady=5)
        
        self.image_label = tk.Label(root)
        self.image_label.grid(row=2, column=0, columnspan=3, sticky="nsew", padx=5, pady=5)
        
        self.status_label = tk.Label(root, text="", font=("Helvetica", 10))
        self.status_label.grid(row=3, column=0, columnspan=3, sticky="nsew", padx=5, pady=5)
        
        self.qr_image = None
        self.current_qr_img = None
        
    def generate_qr(self):
        content = self.content_var.get().strip()
        if not content:
            messagebox.showwarning("Input Error", "Please enter content for the QR code.")
            return
        
        try:
            # Create QR code
            qr = qrcode.QRCode(
                version=None,  # Auto-select version
                error_correction=qrcode.constants.ERROR_CORRECT_H,
                box_size=10,
                border=4,
            )
            qr.add_data(content)
            qr.make(fit=True)
            
            # Generate image
            img = qr.make_image(fill_color="black", back_color="white")
            self.current_qr_img = img  # Save for later saving
            
            # Resize for display
            max_size = (400, 400)
            img.thumbnail(max_size, Image.LANCZOS)
            
            # Convert to PhotoImage for Tkinter
            self.qr_image = ImageTk.PhotoImage(img)
            self.image_label.config(image=self.qr_image)
            self.status_label.config(text=f"QR Code for: {content}")
            
        except Exception as e:
            messagebox.showerror("Error", f"Failed to generate QR code: {str(e)}")
            
    def save_qr(self):
        content = self.content_var.get().strip()
        filename = self.filename_var.get().strip()
        
        if not content:
            messagebox.showwarning("Input Error", "Please generate a QR code first.")
            return
        if not filename:
            messagebox.showwarning("Input Error", "Please enter a file name.")
            return
        if any(char in filename for char in '/\\:*?"<>|'):
            messagebox.showwarning("Input Error", "File name contains invalid characters.")
            return
            
        try:
            # Create QR_Codes directory if it doesn't exist
            save_dir = os.path.join(os.getcwd(), "QR_Codes")
            os.makedirs(save_dir, exist_ok=True)
            
            # Save the QR code
            save_path = os.path.join(save_dir, f"{filename}.png")
            
            if self.current_qr_img:
                # Create a new QR code for saving (full size)
                qr = qrcode.QRCode(
                    version=None,
                    error_correction=qrcode.constants.ERROR_CORRECT_H,
                    box_size=10,
                    border=4,
                )
                qr.add_data(content)
                qr.make(fit=True)
                img = qr.make_image(fill_color="black", back_color="white")
                img.save(save_path)
                
                messagebox.showinfo("Success", f"QR code saved to {save_path}")
            else:
                messagebox.showwarning("Error", "No QR code generated to save")
            
        except Exception as e:
            messagebox.showerror("Error", f"Failed to save QR code: {str(e)}")

if __name__ == "__main__":
    root = tk.Tk()
    app = QRCodeGenerator(root)
    root.mainloop()