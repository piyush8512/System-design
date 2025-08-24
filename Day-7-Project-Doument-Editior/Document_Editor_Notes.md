# Document Editor Example — Notes

## 1) Purpose of the Design
This program demonstrates:
- **OOP concepts**: abstraction, encapsulation, polymorphism.
- **SOLID principles**:
  - **Single Responsibility (SRP):** Each class has one responsibility (e.g., `TextElement` handles text, `FileStorage` handles file saving).
  - **Open/Closed Principle (OCP):** New element types (e.g., `NewLineElement`, `TabSpaceElement`, `TableElement`) can be added **without modifying** existing code.
  - **Dependency Inversion Principle (DIP):** High-level `DocumentEditor` depends on the `Persistence` **abstraction**, not on concrete `FileStorage`.

---

## 2) Key Components

### Interfaces
- **`DocumentElement`**: abstraction for all elements (text, image, newline, tab).
- **`Persistence`**: abstraction for saving the document (file, DB, etc.).

### Concrete Implementations
- **`TextElement`**: renders plain text.
- **`ImageElement`**: renders an image placeholder like `[Image: path]`.
- **`NewLineElement`**: renders a newline (`\n`).
- **`TabSpaceElement`**: renders a tab (`\t`).

### Core Classes
- **`Document`**
  - Maintains a list of `DocumentElement` objects.
  - Provides a `render()` method to concatenate the results of all elements.
- **`FileStorage`**
  - Implements `Persistence` to save the rendered document to `document.txt`.
- **`DBStorage`**
  - Placeholder implementation for saving to a database.
- **`DocumentEditor`**
  - Client-facing API for adding elements (**text, image, newline, tab**).
  - Uses a `Document` to build content and a `Persistence` to save it.
- **`DocumentEditorClient`**
  - Demonstrates usage with text, formatting, rendering, and saving.

---

## 3) Flow of Control
1. **Client** interacts with **`DocumentEditor`**.
2. **`DocumentEditor`** adds elements (`TextElement`, `ImageElement`, etc.) to **`Document`**.
3. **`Document`** **renders** the complete content by concatenating each element’s `render()` output.
4. **`DocumentEditor`** **delegates saving** to the injected **`Persistence`** implementation (e.g., `FileStorage`, `DBStorage`).

---

## 4) Advantages
- **Extensibility**: Easily add new document elements (e.g., `TableElement`, `CodeBlockElement`) via the `DocumentElement` abstraction.
- **Flexibility**: Swap storage to file, DB, or a new option (e.g., `CloudStorage`) **without changing** `DocumentEditor`.
- **Separation of Concerns**: Rendering (elements), storage (persistence), and editing (editor) are **separated**.

---

## 5) Quick SOLID Mapping
- **SRP**: `Document` (collection), `DocumentEditor` (orchestration), `FileStorage/DBStorage` (persistence) each do **one thing**.
- **OCP**: Add new elements or persistence types by **extending**, not modifying existing classes.
- **DIP**: `DocumentEditor` depends on `Persistence` (an interface), not concrete implementations.