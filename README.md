import sys
from PyQt5.QtWidgets import (
    QApplication, QMainWindow, QWidget, QVBoxLayout, QHBoxLayout,
    QPushButton, QLabel, QFileDialog, QScrollArea, QFrame
)
from PyQt5.QtGui import QPixmap
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
        self.layout = QVBoxLayout(self.container)

        # Upload button
        self.upload_btn = QPushButton("Upload Image")
        self.upload_btn.setFixedHeight(40)
        self.upload_btn.clicked.connect(self.upload_image)
        self.layout.addWidget(self.upload_btn)

        # Scroll Area for feed
        self.scroll = QScrollArea()
        self.scroll.setWidgetResizable(True)
        self.feed_widget = QWidget()
        self.feed_layout = QVBoxLayout(self.feed_widget)
        self.feed_layout.setAlignment(Qt.AlignTop)  # Align posts to top
        self.scroll.setWidget(self.feed_widget)
        self.layout.addWidget(self.scroll)

        self.setCentralWidget(self.container)

    def upload_image(self):
        file_name, _ = QFileDialog.getOpenFileName(self, "Select Image", "", "Images (*.png *.jpg *.jpeg)")
        if file_name:
            self.add_post(file_name)

    def add_post(self, image_path):
        post_frame = QFrame()
        post_frame.setStyleSheet("QFrame {background-color: #f5f5f5; border-radius: 10px;}")
        post_layout = QVBoxLayout(post_frame)
        post_layout.setContentsMargins(10,10,10,10)

        # Image
        pixmap = QPixmap(image_path).scaled(350, 350, Qt.KeepAspectRatio, Qt.SmoothTransformation)
        image_label = QLabel()
        image_label.setPixmap(pixmap)
        image_label.setAlignment(Qt.AlignCenter)
        post_layout.addWidget(image_label)

        # Like button
        like_btn = QPushButton("♡ Like")
        like_btn.setCheckable(True)
        like_btn.clicked.connect(lambda state, btn=like_btn: btn.setText("♥ Liked" if state else "♡ Like"))
        post_layout.addWidget(like_btn, alignment=Qt.AlignCenter)

        # Add post to feed
        self.feed_layout.addWidget(post_frame)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = InstagramClone()
    window.show()
    sys.exit(app.exec_())