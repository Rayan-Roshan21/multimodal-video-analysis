#  Multimodal Video Analysis Tool 📹

This React application allows users to input a YouTube video URL, view the video, and generate clickable timestamps for different sections of the video using Google's Generative AI (Gemini).

## Features ✨

-   ✅ **Load YouTube Videos**: Enter a YouTube video URL to load and display the video.
-   ✅ **Generate Timestamps**: Automatically generate timestamps for the video content.
-   ✅ **Clickable Timestamps**: Timestamps are displayed as links that jump to the specific time in the YouTube video.
-   ✅ **Responsive Design**: The application is designed to work on different screen sizes.
-   ✅ **Error Handling**: Displays messages for loading states and errors during timestamp generation.

## Technologies Used 🛠️

-   **React**: A JavaScript library for building user interfaces.
-   **React Bootstrap**: For UI components and styling.
-   **Bootstrap**: CSS framework for responsive design.
-   **Google Generative AI (Gemini)**: Used for generating video timestamps.
-   **JavaScript (ES6+)**
-   **HTML5 & CSS3**

## Getting Started 🚀

### Prerequisites

-   Node.js and npm (or yarn) installed on your machine.
-   A Google Generative AI API key.

### Installation & Setup

1.  **Clone the repository (if applicable) or download the files.**
2.  **Navigate to the project directory:**
    ```bash
    cd multimodal-video-analysis
    ```
    3.  **Install dependencies:**
        ```bash
        npm install
        # or
        # yarn install
        ```

    4.  **Run the application:**
        ```bash
        npm run dev
        # or
        # yarn dev
        ```
        This will open the application in your default web browser, usually at `http://localhost:5173`.

    ## How It Works ⚙️

    1.  **Enter URL**: The user inputs a YouTube video URL into the form.
    2.  **Load Video**: Upon submission, the application extracts the video ID and embeds the YouTube player.
    3.  **Generate Timestamps**:
        *   When the "Generate Timestamps" button is clicked, the application sends a request to the Google Generative AI API.
        *   The request includes a prompt asking the AI to create timestamps in the format "MM:SS - title" or "HH:MM:SS - title" and the video file URI (constructed from the YouTube video ID).
        *   The AI processes the video content and returns a text response with the generated timestamps.
    4.  **Process and Display Timestamps**:
        *   The application parses the AI's response, extracting lines that match the expected timestamp format.
        *   It converts the time (e.g., "01:23") into total seconds.
        *   Each valid timestamp is then converted into a clickable link that directs the user to the specific point in the YouTube video.
        *   The processed timestamps are displayed below the video player.

    ## Code Overview (`src/App.jsx`) 💻

    -   **State Variables**:
        -   `videoUrl`: Stores the embeddable YouTube video URL.
        -   `videoId`: Stores the extracted YouTube video ID.
        -   `timestamps`: An array to store the generated timestamp objects (each with `displayText` and `url`).
        -   `loading`: Boolean to indicate if timestamps are being generated.
        -   `error`: String to store any error messages.
    -   **`handleSubmit(e)`**:
        -   Prevents default form submission.
        -   Extracts the video ID from various YouTube URL formats.
        -   Updates `videoUrl` and `videoId` state.
        -   Clears previous timestamps.
    -   **`generateTimestamps()`**:
        -   Async function to interact with the Google Generative AI API.
        -   Uses the API key from environment variables.
        -   Sends a prompt and the video file URI to the Gemini model.
        -   Parses the text response from the AI to extract timestamps.
        -   Converts timestamps to clickable links.
    -   **Return (JSX)**:
        -   Renders the main layout with a title.
        -   A form to input the YouTube URL.
        -   An `iframe` to embed the YouTube video player.
        -   A button to trigger `generateTimestamps`.
        -   Displays loading spinner, error messages, or the list of generated timestamps.

    ## Customization 🎨

    -   **Styling**: The application uses Bootstrap for styling, which can be customized as needed.
    -   **AI Prompt**: The prompt sent to the Google Generative AI can be modified in the `generateTimestamps` function to change how timestamps are generated or formatted.
    -   **Timestamp Parsing**: The regular expressions and logic for parsing timestamps can be adjusted if the AI's output format changes or if a different format is desired.
