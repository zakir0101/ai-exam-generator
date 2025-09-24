
# AI Exam Question Generator

Welcome to the AI Exam Question Generator project! This repository contains the source code for a modern web application designed to help students and educators create interactive quizzes from study materials using the power of Google's Gemini API.

## 🎯 Project Purpose

The primary goal of this project is to provide a user-friendly tool that can take various forms of content (PDFs, text files, presentations, and even audio/video) and automatically generate a variety of exam-style questions. This helps automate the tedious process of creating study guides and practice tests, making learning more efficient and interactive.

## ✨ Core Features (TODO)

- [ ] **Project Foundation**: Set up the basic HTML structure, styling, and React component shell.
- [ ] **Static UI Form**: Build the main configuration user interface.
- [ ] **File Parsing**: Implement utility functions to extract text from various file formats (`.pdf`, `.pptx`, `.txt`).
- [ ] **State Management**: Wire up the UI form to React state.
- [ ] **Gemini Service**: Integrate the Gemini API to generate questions based on user input and `responseSchema`.
- [ ] **Interactive Quiz Mode**: Build the component for taking a standard, self-paced quiz.
- [ ] **Results & Review**: Create the screen to display the final score and review answers.
- [ ] **Live Audio Quiz Mode**: Implement the voice-driven quiz feature using Gemini's native audio capabilities.
- [ ] **Final Polish**: Refine styling, add animations, and ensure full responsiveness and accessibility.

## 🛠️ Tech Stack

This project is built as a modular, client-side React application , making it easy to run and develop.

-   **Framework**: [React](https://reactjs.org/) (loaded via CDN)
-   **Styling**: [Tailwind CSS](https://tailwindcss.com/) (loaded via CDN)
-   **AI Integration**: [Google Gemini API](https://ai.google.dev/) via the `@google/genai` library.
-   **File Parsing**:
    -   [PDF.js](https://mozilla.github.io/pdf.js/) for PDF text extraction.
    -   [JSZip](https://stuk.github.io/jszip/) for parsing `.pptx` files.
-   **Language**: TypeScript (transpiled in-browser via Babel)

## 🚀 Getting Started

See the `CONTRIBUTING.md` file for guidelines on how to contribute to the project.
more info about how to build and run this project should be added/updated after each PR (if changed)
