
# Contributing to the AI Exam Question Generator

First off, thank you for considering contributing! This project thrives on community effort, and every contribution is valued.

This document provides guidelines for contributing to the project to ensure a smooth and collaborative development process.

## 💻 How to Contribute

1.  **Find an Issue:** Look for an open issue in the [Issues tab](https://github.com/your-repo/ai-question-generator/issues). The issues are structured as a step-by-step guide to building the app. It's best to tackle them in order. If you want to work on one, please comment on it to claim it.
2.  **Fork the Repository:** Create your own fork of the repository to your GitHub account.
3.  **Create a Branch:** Create a new branch in your forked repository for your feature or bug fix. Please name your branch descriptively.
    -   Example: `feat/add-configuration-form` or `fix/quiz-scoring-bug`
4.  **Write Code:** Make your changes, adhering to the code style and best practices outlined below.
5.  **Commit Your Changes:** Write clear, concise commit messages. We follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification.
    -   `feat:` A new feature.
    -   `fix:` A bug fix.
    -   `docs:` Documentation only changes.
    -   `style:` Changes that do not affect the meaning of the code (white-space, formatting, etc).
    -   `refactor:` A code change that neither fixes a bug nor adds a feature.
    -   `chore:` Changes to the build process or auxiliary tools.
6.  **Submit a Pull Request:** Open a pull request from your branch to the `main` branch of the original repository. Please provide a detailed description of the changes you've made.

## ✨ Code Style & Best Practices

-   **Modularity:** Keep files small and focused on a single responsibility. A component file should only contain the component, a service file should only handle API calls, etc.
-   **Readability:** Use clear and descriptive names for variables, functions, and components. Write comments for complex or non-obvious logic.
-   **Styling:** All styling must be done using **Tailwind CSS classes only**. Do not write custom CSS in `<style>` tags or `.css` files.
-   **State Management:** State that is shared between multiple components should be lifted up to the nearest common ancestor (e.g., `App.tsx`). Component-specific state should remain local.
-   **Error Handling:** Gracefully handle potential errors, especially from API calls, and provide clear feedback to the user.
-   **Accessibility:** Use semantic HTML and ARIA attributes where necessary to ensure the application is usable by everyone.

Thank you again for your contribution!
