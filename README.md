 Project Documentation: QR Code Generator in Python
1. General Information
Project Name: QR Code Generator
Programming Language: Python 3.x
Development Environment: PyCharm
Interface Type: Graphical User Interface (GUI)
Purpose: A utility to create QR codes based on user-input text and save them as PNG image files.

This project is a desktop application with a graphical interface built using Tkinter. It allows users to input any text, generate a QR code from it, preview the result, and save it to disk.

2. Technologies and Libraries Used
Tkinter – Python’s built-in library for building desktop GUI applications.

qrcode – A third-party library for generating QR codes, supporting various error correction levels.

Pillow (PIL) – A library for image processing and resizing.

os – A built-in Python module for interacting with the file system.

io.BytesIO – A module used for handling byte streams in memory.

messagebox – A Tkinter module for showing warning, error, and info pop-up dialogs.

3. Features
The program provides the following key features:

Input field for text to be encoded into a QR code.

On-screen display (preview) of the generated QR code.

File name input for saving the QR image.

QR code saving in .png format into a folder named QR_Codes, created automatically.

Input validation (e.g., disallowing forbidden characters in file names).

Error and success messages via pop-ups.

4. Project Structure
Once launched, the project consists of a single main file:

css
Копировать
Редактировать
QRCodeGenerator/
├── main.py         ← main application file
└── QR_Codes/       ← created automatically upon saving a QR code
5. Core Components
Class: QRCodeGenerator
This is the main class of the application, responsible for setting up the interface and managing functionality.

__init__(self, root)
Configures the main Tkinter window.

Creates and places GUI elements: input fields, buttons, labels.

Uses a grid layout for a responsive and scalable interface.

generate_qr(self)
Retrieves the user’s input text.

Generates a QR code using the qrcode library.

Resizes the image for preview.

Displays the image in the GUI using ImageTk.

save_qr(self)
Validates the presence of text and file name.

Checks that the file name does not include forbidden characters (/\:*?"<>|).

Creates the QR_Codes/ directory if it does not exist.

Regenerates the QR code at full size and saves it as a .png file.

Displays a success message.

6. How to Use
Run main.py.

Enter the text you want to encode into a QR code.

Click Generate QR.

Enter a file name (e.g., my_qr_code).

Click Save QR.

Open the QR_Codes folder — you will find the image my_qr_code.png.

7. Potential Improvements
This application can be expanded with additional features in the future:

Custom color options for QR code and background.

Add a logo (e.g., brand logo) to the center of the QR code.

Batch generation from a list of inputs.

Export options to other formats (PDF, SVG).

Mobile version for Android/iOS using Kivy or Flutter.

QR code generation history using a database (e.g., SQLite).

8. Conclusion
The QR Code Generator project is a practical and easy-to-use tool built with Python. By leveraging modern libraries and a clear GUI, the application offers a user-friendly experience for generating and saving QR codes. It is suitable for both educational and practical uses. Developing and maintaining the project in PyCharm ensures ease of debugging, testing, and future upgrades.

