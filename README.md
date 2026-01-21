# MNIST From Scratch (C)

## Original Source / Inspiration (Credit First)
This project is based on and inspired by **Ian Dvorin (Magicalbat)** and his work shared on GitHub:

- **Ian Dvorin (Magicalbat)**: https://github.com/Magicalbat

The original implementation style, structure, and idea of building ML systems in pure C with low-level tools was taken from his work and used as the learning foundation for this repository.

---

## Why I Built This
I created this repository as my first serious "from scratch" machine learning implementation in **C**, to deeply understand what happens behind common ML libraries like PyTorch and TensorFlow.

My goal was not just to "train a model", but to learn how the full ML pipeline works at a low level:

- how data is represented in memory
- how matrix operations are implemented manually
- how forward passes are computed
- how gradients flow backwards (backpropagation)
- how training updates parameters

This project is mainly educational and meant to document my learning journey in systems programming + machine learning fundamentals.

---

## What This Project Does
This repository implements an MNIST digit classifier in C, including:

- A custom **matrix** type (`rows`, `cols`, row-major `data`)
- Core **matrix operations**
  - addition / subtraction
  - matrix multiplication (with transpose options)
  - ReLU activation
  - Softmax
  - Cross entropy loss
- A lightweight "model graph" / program execution structure
  - forward program construction
  - cost program construction
  - gradient computation through backpropagation
- A full training loop using MNIST dataset

---

## Results

### ASCII Visualization of MNIST Digit
![MNIST Digit Visualization](screenshots/mnist_digit.png)

The program displays MNIST digits as ASCII art before training begins.

---

### Training Progress
![Training Progress](screenshots/training_progress.png)

The model trains for 10 epochs, achieving **93.2% test accuracy** on the MNIST test set.

Key metrics:
- **Final Test Accuracy**: 93.22% (9322/10000)
- **Top-3 Accuracy**: 98.71%
- Training loss decreases from ~0.61 to ~0.23 over 10 epochs

---

### Confusion Matrix & Per-Class Accuracy
![Confusion Matrix](screenshots/confusion_matrix.png)

Per-digit accuracy breakdown:
- **Best performance**: Digit 0 (98.27%), Digit 1 (97.44%)
- **Most challenging**: Digit 5 (88.23%), Digit 8 (89.94%), Digit 9 (88.40%)

The confusion matrix shows common misclassifications (e.g., 5→3, 8→3, 9→4).

---

## My Contributions (What I Personally Implemented / Organized)
Even though the original inspiration and codebase style came from Ian Dvorin, the work inside *this repo* reflects my own setup and learning implementation process.

### ✅ 1) Built and organized the full runnable project folder
I created a clean repo layout that contains everything needed to build and run the project locally:

- `main.c` (model + training loop)
- `arena.c / arena.h` (custom memory arena)
- `prng.c / prng.h` (random generator for weight initialization)
- `base.h` (type system + macros)
- `mnist.py` (dataset export to `.mat` binary format)

---

### ✅ 2) Integrated a custom memory arena system
I included a full arena allocator (`arena.c / arena.h`) used throughout the project for fast memory allocation, including:

- reserve/commit memory model
- push/pop allocation
- temporary arenas
- scratch arenas for intermediate computations

This approach avoids frequent heap allocations and helps keep memory usage predictable.

---

### ✅ 3) Implemented dataset export pipeline
I used Python (`mnist.py`) to export MNIST into raw binary `.mat` files used by the C program:

- `train_images.mat`
- `train_labels.mat`
- `test_images.mat`
- `test_labels.mat`

This makes the C implementation fully independent from Python during training and inference.

---

### ✅ 4) Created GitHub-ready project setup
To make the project clean and professional on GitHub, I set up version control behavior including a `.gitignore` to avoid committing unnecessary build artifacts:

Ignored:
- compiled binaries (`*.exe`, `*.out`)
- object files (`*.o`)
- generated dataset binaries (`*.mat`)
- vscode metadata (`.vscode/`)

This keeps the repository lightweight and readable.

---

## Files Overview
- **`main.c`**  
  Main neural network implementation (model graph, forward pass, gradients, training loop).

- **`arena.c` / `arena.h`**  
  Memory arena allocator system for fast allocations.

- **`prng.c` / `prng.h`**  
  Random number generator used for initializing weights.

- **`base.h`**  
  Types, math helpers, and macros (KiB/MiB/GiB, MIN/MAX, alignment helpers).

- **`mnist.py`**  
  Downloads MNIST and exports raw binary arrays to `.mat` files.

---

## How To Run

### 1) Generate MNIST `.mat` files (Python)
Install dependencies:
```bash
pip install numpy tensorflow-datasets
```

Run:
```bash
python mnist.py
```

This will generate:
- `train_images.mat`
- `train_labels.mat`
- `test_images.mat`
- `test_labels.mat`

### 2) Compile (C)
Example (clang):
```bash
clang main.c -O3 -lm
```

Or (gcc):
```bash
gcc main.c -O3 -lm
```

### 3) Run
```bash
./a.exe
```

You should see:
- an ASCII visualization of an MNIST digit
- pre-training output predictions
- training progress across epochs/batches
- post-training output predictions
- confusion matrix and per-class accuracy

---

## Notes
- This is an educational project and may not be optimized for production ML performance.
- The goal is clarity and understanding of low-level ML mechanics in C.
- Attribution is included above to credit the original inspiration source.

---

## License
This repository includes an MIT License file.

Original inspiration credited to:  
**Ian Dvorin (Magicalbat)** — https://github.com/Magicalbat
