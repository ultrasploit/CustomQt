# CustomQt

CustomQt is a lightweight Python library that allows you to create **native custom titlebars on Windows** using **PySide6**. It provides frameless windows, custom hit-testing, rounded corners, and optional acrylic blur effects, while keeping the native window controls fully functional.

---

## Features

* Fully **frameless window** support on Windows.
* Custom **titlebar hit-testing** for drag and resize.
* **Rounded corners** compatible with Windows 11.
* **Acrylic blur** effect for modern Windows aesthetics.
* Automatic handling of **maximize, restore, and cursor states**.
* Debounced corner updates to reduce flicker on resize.
* Safe fallback to native title bar behavior.

---

## Installation

Install using pip (PySide6 is required):

```bash
pip install PySide6
```

Then include CustomQt in your project (assuming you package it as `customqt`).

---

## Usage

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton
from customqt import WindowsStyler

app = QApplication([])

window = QWidget()
window.resize(800, 600)

# Initialize the custom Windows styler
styler = WindowsStyler(
    window,
    titlebar_fallback=True,            # Enable fallback draggable area
    titlebar_fallback_height=30,       # Height of fallback title bar
    border_width=8,                    # Resizable border width
    round_corner_radius=15             # Rounded corner radius
)
styler.init()

# Optional: connect your maximize button
maximize_btn = QPushButton("⬜", window)
styler.setTitlebarMaximizeButton(maximize_btn)

window.show()
app.exec()
```

---

## API

### `WindowsStyler`

#### Parameters:

* `window: QWidget` – The target window to customize.
* `hittest_callback: Optional[Callable[[QPoint], Optional[Tuple[bool, int]]]]` – Optional callback for custom hit-testing.
* `border_width: int = 8` – Width of resizable window borders.
* `titlebar_fallback: bool = True` – Enable fallback draggable titlebar.
* `titlebar_fallback_height: int = 30` – Height of fallback draggable area.
* `round_corner_radius: int = 15` – Radius for window rounded corners.

#### Methods:

* `init()` – Initialize the styler. Must be called before showing the window.
* `setTitlebarMaximizeButton(button: QPushButton)` – Assign a maximize/restore button to update its state automatically.
* `showMaximized()` – Maximize the window and remove rounded corners.
* `showNormal()` – Restore the window and apply rounded corners.
* `isMaximized() -> bool` – Check if the window is currently maximized.
* `apply_rounded_corners()` – Manually apply rounded corners.
* `enable_acrylic_blur()` – Enable acrylic blur behind the window.
* `cleanup()` – Clean up resources (timers, cursor) when the window is destroyed.

---

## Notes

* **Platform:** Windows only. Attempting to use this library on other platforms will raise an error.
* **Windows 11:** Automatically uses native rounded corners if available; otherwise falls back to manual rounding.
* **Performance:** Debounced corner updates prevent excessive redrawing during resizing or snapping.

---

## License

MIT License – Feel free to use, modify, and distribute.
