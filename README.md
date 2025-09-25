# app.py
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QVBoxLayout, QLineEdit, QLabel

class DemoApp(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("PyQt5 Demo App")
        self.setGeometry(200, 200, 400, 200)

        self.layout = QVBoxLayout()

        self.label = QLabel("Type something below:", self)
        self.input = QLineEdit(self)
        self.button = QPushButton("Submit", self)

        self.button.clicked.connect(self.show_text)

        self.layout.addWidget(self.label)
        self.layout.addWidget(self.input)
        self.layout.addWidget(self.button)

        self.setLayout(self.layout)

    def show_text(self):
        text = self.input.text()
        self.label.setText(f"You typed: {text}")

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = DemoApp()
    window.show()
    sys.exit(app.exec_())







# auto.py
import pyautogui
import time

pyautogui.FAILSAFE = True
pyautogui.PAUSE = 0.3

def main():
    print("Switch to the PyQt5 app window! Starting in 3 seconds...")
    time.sleep(3)

    # Type into the input field
    pyautogui.write("Hello PyQt5", interval=0.1)

    # Move focus to button (Tab once)
    pyautogui.press("tab")

    # Press Enter to click button
    pyautogui.press("enter")

if __name__ == "__main__":
    main()