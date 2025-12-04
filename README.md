# CustomQt

**CustomQt** is a lightweight Python library for **PySide6** that enables **native-feeling custom titlebars and frameless windows**.  
It currently supports **Windows**, with planned support for **Linux** and **macOS**.

The goal of CustomQt is to provide a clean, customizable alternative to Qt’s default window chrome—**without losing native drag, resize, maximize, shadows, or system behaviors**.

---

## ✨ Features (Current & Planned)

### ✔ Currently implemented (Windows)
- Fully **frameless window** support  
- Accurate **native hit-testing** (drag, resize, corners)  
- **Rounded corners** with Windows 11 support  
- Optional **Acrylic blur** / Mica effect  
- Native handling of **maximize / restore / resize states**  
- Debounced corner updates to reduce flicker  
- Customizable titlebar fallback area  

### 🚧 Planned (Linux / macOS)
- Wayland-compatible client-side decorations  
- X11 support using EWMH/NETWM hints  
- GNOME/KDE-compatible shadows + resize edges  
- macOS vibrancy & blending effects  
- Cross-platform custom maximize/minimize buttons  
- Unified API across all supported OSes  

---

## 📦 Installation

Install PySide6:

```bash
pip install PySide6
```

Import CustomQt (once packaged):

```python
from customqt import WindowsStyler
```

---

## 🚀 Usage Example (Windows)

```python
from PySide6.QtWidgets import QApplication, QWidget, QPushButton
from customqt import WindowsStyler

app = QApplication([])

window = QWidget()
window.resize(800, 600)

styler = WindowsStyler(
    window,
    titlebar_fallback=True,
    titlebar_fallback_height=30,
    border_width=8,
    round_corner_radius=15
)
styler.init()

maximize_btn = QPushButton("⬜", window)
styler.setTitlebarMaximizeButton(maximize_btn)

window.show()
app.exec()
```

---

## 🧩 API Reference

### `WindowsStyler` (Windows)

#### **Parameters**
- `window: QWidget`
- `hittest_callback: Optional[Callable]`
- `border_width: int = 8`
- `titlebar_fallback: bool = True`
- `titlebar_fallback_height: int = 30`
- `round_corner_radius: int = 15`

#### **Methods**
- `init()`
- `setTitlebarMaximizeButton(button)`
- `showMaximized()`
- `showNormal()`
- `isMaximized() -> bool`
- `apply_rounded_corners()`
- `enable_acrylic_blur()`
- `cleanup()`

---

## 🖥️ Platform Support

### ✔ Windows — Supported
The Windows implementation uses native APIs such as:
- DWM (shadows, accents, blur)  
- `WM_NCHITTEST` (resize/drag)  
- DPI-aware frame metrics  
- Rounded corner policies  

### 🐧 Linux — Planned
Linux support will require:
- Wayland CSD protocols (xdg-decoration, ext-…)  
- X11 EWMH hints, `_MOTIF_WM_HINTS`, `_NET_WM` sizing  
- Handling KDE/Mutter differences  
- Qt platform plugin integration  

**Contributors with Linux WM knowledge are very welcome!**

### 🍎 macOS — Future
Planned features:
- Vibrancy  
- Titlebar blending  
- Custom system button areas  
- Resize semantics  

---

## 💬 Contributing

Contributions are welcome!  
Especially from developers experienced in:
- Wayland/X11 window manager internals  
- Qt QPA platform plugins  
- macOS window management APIs  

Feel free to open issues, discussions, or PRs.

---

## 📄 License

MIT License — free for personal and commercial use.
