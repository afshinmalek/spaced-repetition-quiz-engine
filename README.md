# Spaced Repetition Quiz Engine

A C++ command-line study tool I built to prep for technical interviews — it quizzes you on
algorithms and machine-learning systems questions, tracks your streaks, and only retests
you on the questions you haven't mastered yet.

🎬 **Demo video:** https://www.youtube.com/watch?v=xKMJOttTDPc

## Features

- **Two quiz decks** — algorithms/data structures and ML/systems, loaded from CSV datasets
- **Spaced repetition** — questions you answer correctly build a streak; only low-streak
  questions come up again, and a streak of 2+ means you've mastered the card
- **Persistent progress** — streaks are saved back to the CSV files on exit, so progress
  carries across sessions
- **Binary search lookup** — find any question instantly by ID
- **Session statistics** — accuracy, correct/incorrect counts after every session
- **Hints** — each quiz module gives topic-specific hints (press `h` during a question)

## Design highlights

- **OOP with inheritance & polymorphism** — abstract `StudyModule` base class with a pure
  virtual `displayHint()`, overridden by `AlgorithmQuiz` and `MachineLearningQuiz`
- **Manual memory management** — the question deck is a dynamically allocated array
  (`new[]`/`delete[]`) with a virtual destructor for safe cleanup through base pointers
- **Classic algorithms** — bubble sort to keep the deck ordered, binary search for ID lookup
- **File I/O** — custom CSV parsing for loading question banks and persisting progress

## Project structure

```
├── main.cpp                 # Menu-driven CLI entry point
├── StudyModule.h / .cpp     # Base class: deck management, sessions, search, persistence
├── Question.h               # Question struct (id, topic, prompt, answer, streak)
├── algorithms_questions.csv # Algorithms & data structures question bank
└── ml_systems_questions.csv # ML & systems design question bank
```

## Build & run

Requires a C++17 compiler (g++ or clang).

```bash
g++ -std=c++17 -o quiz main.cpp StudyModule.cpp
./quiz
```

Then pick a deck from the menu:

```
=======================================
   CS & AI SPACED REPETITION ENGINE
=======================================
1. Start Algorithm Quiz
2. Start Machine Learning Quiz
3. Search for Question by ID
4. Save Progress & Exit
```

## How the spaced repetition works

Each question carries a `streak` counter. Answer correctly and the streak increments;
get it wrong and it resets to zero. Study sessions skip anything with a streak of 2 or
higher, so your time goes to the material you haven't nailed yet. Streaks persist in the
CSV files between runs.

## Possible improvements

- Smarter scheduling (e.g. SM-2 intervals instead of a fixed streak threshold)
- Decouple the question banks from progress state (separate data vs. save files)
- Replace the fixed-capacity array with `std::vector` for safer dynamic growth
- Unit tests for the search/sort/persistence logic

---
*Originally built as a final project for CIS 25 (C++ Programming).*
