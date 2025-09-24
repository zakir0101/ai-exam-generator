[this file contain an overview of the estimated final project .. it does not apply to the current status of the project .. if you are interested in acommplising a specifc task or issue .. you could just read this to grasp how everything might look at the end just to inspire and orient your self ... for each specific issue please try to stick to the current provided instructions ]

#  Replicate the AI Exam Question Generator Application

## 1. High-Level Overview

**Application Name:** Interactive Exam Question Generator

**Core Purpose:** To create an interactive web application that helps students prepare for exams. Users can upload their study materials (documents, audio, video), and the application uses the Google Gemini API to generate a variety of quiz questions based on the content.

**Key Features:**
-   **File Upload:** Supports uploading various study materials, including PDF, TXT, PPTX, and common audio/video formats.
-   **Quiz Configuration:** Allows users to set their Gemini API key, choose question types (True/False, Multiple Choice, Matching), specify the number of questions, and set a difficulty level.
-   **AI-Powered Question Generation:** Communicates with the Gemini API to analyze the provided content and generate a structured quiz in JSON format.
-   **Dual Quiz Modes:**
    1.  **Interactive Mode:** A standard, self-paced quiz where users click to select answers.
    2.  **Live Audio Mode:** An immersive, voice-driven quiz where the user interacts with an AI "game show host" using their microphone.
-   **Results & Review:** Provides a detailed results screen with a final score, a performance message, and a question-by-question review of the user's answers against the correct ones.
-   **Modular & Extensible:** Built with a clean, modular architecture in React.

---

## 2. Visual Design & UI/UX

**Overall Aesthetic:**
-   **Theme:** Modern, clean, and professional with a focus on usability.
-   **Layout:** A responsive, single-page application design.
-   **Color Palette:**
    -   Background: Light Gray (`bg-gray-100`).
    -   Content Panels: White with rounded corners and soft shadows (`bg-white p-8 rounded-xl shadow-lg`).
    -   Primary Accent: Indigo (`bg-indigo-600` for buttons, text-indigo-600 for highlights).
    -   Secondary Accent: Purple (`bg-purple-600`) for the Live Quiz button.
    -   Success: Green (for correct answers, success messages).
    -   Error: Red (for incorrect answers, error messages).
-   **Typography:** 'Poppins' from Google Fonts. Text is generally dark gray (`text-gray-800`).
-   **Interactivity:** Smooth transitions (`fade-in` animation for new screens) and clear hover/focus states on interactive elements.

**Layout Structure:**
1.  **Header:**
    -   Sticky to the top of the viewport.
    -   White background with a `shadow-sm`.
    -   Contains the main title "Interactive Exam Question Generator" (large, bold, indigo) and a descriptive subtitle.
2.  **Main Content:**
    -   A centered container that dynamically renders the current view (Configuration, Quiz, Results, etc.) based on the application's state.
3.  **Footer:**
    -   Simple, centered text at the bottom with a copyright notice.

---

## 3. Component-by-Component Screen Descriptions

The application flow is managed by a state machine. Describe the UI for each state:

### 3.1. Configuration Screen (`AppState.CONFIGURING`)
This is the initial and main setup view, presented as a single, multi-step card.

-   **Section 1: API & Model:**
    -   **Gemini API Key:** A password input field.
    -   **Model:** A select dropdown, pre-filled and locked to `gemini-2.5-flash`.
-   **Section 2: Upload Study Material:**
    -   A large file drop zone with a dashed border.
    -   **Empty State:** Shows an upload icon and text prompts ("Click to upload", "PDF, TXT, PPTX...").
    -   **Filled State:** When files are added, it lists their names and provides a "Clear All" button.
-   **Section 3: Configure Your Quiz:**
    -   **Question Types:** A grid of custom-styled checkboxes for "True/False", "Multiple Choice", and "Matching". Selected options have an indigo border.
    -   **Number of Questions:** A standard number input.
    -   **Difficulty Level:** A select dropdown with "Easy", "Medium", "Hard".
-   **Section 4: Generate Button:**
    -   A large, full-width, indigo button labeled "Generate Quiz".
    -   It is disabled until all necessary fields (API key, file, question types) are provided.
    -   During generation, it shows a spinner and the text "Generating Questions...".
-   **Status/Error Area:**
    -   A dedicated section at the bottom displays contextual messages. Blue for status updates (e.g., "Processing file...") and red for errors.

### 3.2. Ready Screen (`AppState.READY`)
This screen appears after the AI has successfully generated the questions.

-   A centered card with a large green checkmark icon.
-   A header "Questions Ready!".
-   Two prominent buttons side-by-side:
    1.  `Start Interactive Quiz` (indigo).
    2.  `Start Live Audio Quiz` (purple). This button is disabled if the quiz contains "Matching" questions, with a tooltip explaining why.

### 3.3. Interactive Quiz Screen (`AppState.QUIZ`)
The standard quiz-taking interface.

-   Displays one question at a time in a clean card layout.
-   **Progress Bar:** A thin progress bar at the top visually tracks completion.
-   **Question Display:** The question text is displayed clearly.
-   **Answer Area (Dynamic):**
    -   **True/False:** Two large, clickable radio button labels for "True" and "False".
    -   **Multiple Choice:** A list of clickable radio button labels for each option.
    -   **Matching:** A two-column layout. The left column lists "premises." The right column has a dropdown for each premise, containing all possible "responses" in a shuffled order.
-   **Navigation:** "Previous" and "Next" buttons. The "Next" button becomes a green "Finish Quiz" button on the final question.

### 3.4. Live Audio Quiz Screen (`AppState.LIVE_QUIZ`)
An immersive, voice-controlled quiz.

-   The UI displays the current question and options for visual reference, but they are not clickable.
-   The styling of the options dynamically updates to show what the user selected (indigo), if it was correct (green), or incorrect (red) after confirmation.
-   **AI Host Section:** A dedicated area at the bottom shows:
    -   The AI's name: "Gennie, The Game Show Host".
    -   The current status (e.g., "Connecting...", "Listening...") next to a microphone icon that turns red when active.
    -   An italicized transcript of what the AI host is saying.
    -   Any error messages.

### 3.5. Results Screen (`AppState.RESULTS`)
The final screen summarizing the user's performance.

-   **Top Card (Score Summary):**
    -   "Quiz Complete!" title.
    -   A dynamic message based on performance (e.g., "Excellent!").
    -   The final score is displayed prominently as a large percentage (e.g., `85%`) and a fraction (e.g., `17 / 20 correct`).
-   **Bottom Card (Answer Review):**
    -   A detailed list of every question.
    -   For each question, it shows the user's answer and the correct answer.
    -   The user's answer is highlighted in green if correct or red if incorrect.
-   **Action Buttons:** "Restart Quiz" and "Create New Quiz" buttons at the very bottom.

---

## 4. Core Functionality & Logic

-   **State Management:** The entire application is controlled by a central state manager in the main `App.tsx` component using React hooks. The `appState` variable is key to rendering the correct view.
-   **File Parsing (`src/utils/fileParsers.ts`):**
    -   Uses `pdf.js` to extract text from PDF files.
    -   Uses `JSZip` to parse `.pptx` files by unzipping them and extracting text from the slide XML.
    -   Handles plain text and converts audio/video files to base64 for the multimodal model.
-   **Gemini API Service (`src/services/geminiService.ts`):**
    -   Constructs a detailed prompt for the Gemini API.
    -   **Crucially, it uses the `responseSchema` feature to force the API to return a predictable JSON structure.** This is the backbone of the application's reliability.
    -   The schema is built dynamically based on the question types selected by the user.
    -   Includes robust error handling for API calls.
-   **Live Quiz Engine (`src/components/quiz/LiveQuiz.tsx`):**
    -   Utilizes the `@google/genai` library's `getLiveClient()` for native audio interaction.
    -   The model used is `gemini-2.5-flash-native-audio-preview-09-2025`.
    -   Manages the audio stream from the user's microphone.
    -   Uses a system of `tools` (`select_answer`, `assure_selection`, `next_question`) to programmatically control the quiz flow based on the AI's understanding of the user's speech. This creates a structured, turn-based conversation.

---

## 5. Technical Stack & Architecture

-   **Frontend Framework:** React (v18) using in-browser JSX transpilation via Babel. No build step is required.
-   **Styling:** Tailwind CSS.
-   **Dependencies (loaded via CDN in `index.html`):**
    -   React, ReactDOM, Babel
    -   `@google/genai`
    -   `pdf.js`
    -   `jszip`
-   **Architecture (Modular):**
    -   `src/`: Main source directory.
    -   `src/index.tsx`: Application entry point.
    -   `src/App.tsx`: The root component, managing state and routing between views.
    -   `src/components/`: Directory for all UI components, organized into subdirectories like `quiz/` and `icons/`.
    -   `src/services/`: For API interaction logic.
    -   `src/utils/`: For helper functions (e.g., file parsers).
    -   `src/constants/`: For application-wide constants (e.g., `AppState`).
    -   `src/types/`: Centralized TypeScript type definitions.
-   **Permissions:** The application requires `microphone` permission, which is declared in `metadata.json`.

