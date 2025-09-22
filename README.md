# coursera-test
Coursera test repository
import sys
import os
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QWidget, QVBoxLayout, QHBoxLayout,
    QPushButton, QLabel, QFileDialog, QScrollArea, QFrame
)
from PyQt5.QtGui import QPixmap, QIcon
from PyQt5.QtCore import Qt

class InstagramClone(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Mini Instagram")
        self.setGeometry(100, 100, 400, 600)
        self.initUI()

    def initUI(self):
        # Main container widget
        self.container = QWidget()
        self.layout = QVBoxLayout()
        self.container.setLayout(self.layout)

        # Scroll Area for feed
        self.scroll = QScrollArea()
        self.scroll.setWidgetResizable(True)
        self.feed_widget = QWidget()
        self.feed_layout = QVBoxLayout()
        self.feed_widget.setLayout(self.feed_layout)
        self.scroll.setWidget(self.feed_widget)

        # Upload button
        self.upload_btn = QPushButton("Upload Image")
        self.upload_btn.clicked.connect(self.upload_image)

        # Add to main layout
        self.layout.addWidget(self.upload_btn)
        self.layout.addWidget(self.scroll)

        self.setCentralWidget(self.container)

    def upload_image(self):
        file_name, _ = QFileDialog.getOpenFileName(self, "Select Image", "", "Images (*.png *.jpg *.jpeg)")
        if file_name:
            self.add_post(file_name)

    def add_post(self, image_path):
        post_frame = QFrame()
        post_layout = QVBoxLayout()
        post_frame.setLayout(post_layout)
        post_frame.setFrameShape(QFrame.StyledPanel)
        post_frame.setStyleSheet("QFrame {background-color: #f5f5f5; border-radius: 10px;}")

        # Image
        pixmap = QPixmap(image_path).scaled(350, 350, Qt.KeepAspectRatio, Qt.SmoothTransformation)
        image_label = QLabel()
        image_label.setPixmap(pixmap)
        image_label.setAlignment(Qt.AlignCenter)

        # Like button
        like_btn = QPushButton("♡ Like")
        like_btn.setCheckable(True)
        like_btn.clicked.connect(lambda state, btn=like_btn: btn.setText("♥ Liked" if state else "♡ Like"))

        # Add to post layout
        post_layout.addWidget(image_label)
        post_layout.addWidget(like_btn)

        # Add post to feed
        self.feed_layout.addWidget(post_frame)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = InstagramClone()
    window.show()
    sys.exit(app.exec_())