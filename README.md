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
    cd your-project-directory
    ```
3.  **Install dependencies:**
    ```bash
    npm install
    # or
    # yarn install
    ```
4.  **Set up Google Generative AI API Key:**
    Open `src/App.js` and replace the placeholder for the API key in the `GoogleGenerativeAI` constructor:
    ```javascript
    // Inside the generateTimestamps function
    const genAI = new GoogleGenerativeAI("YOUR_API_KEY_HERE");
    ```
    **Note:** 🔑 It's highly recommended to use environment variables for API keys in a production environment or a more secure setup.

5.  **Run the application:**
    ```bash
    npm start
    # or
    # yarn start
    ```
    This will open the application in your default web browser, usually at `http://localhost:3000`.

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
    *   Each valid timestamp is then converted into a clickable link that directs the user to the specific point in the YouTube video (`https://www.youtube.com/watch?v=VIDEO_ID&t=SECONDSs`).
    *   The processed timestamps are displayed below the video player.

## Code Overview (`src/App.js`) 💻

-   **State Variables**:
    -   `videoUrl`: Stores the embeddable YouTube video URL.
    -   `videoId`: Stores the extracted YouTube video ID.
    -   `timestamps`: An array to store the generated timestamp objects (each with `displayText` and `url`).
    -   `loading`: Boolean to indicate if timestamps are being generated.
    -   `error`: String to store any error messages.
-   **`handleSubmit(e)`**:
    -   Prevents default form submission.
    -   Extracts the video ID from various YouTube URL formats (standard watch URL, shortened youtu.be URL).
    -   Updates `videoUrl` and `videoId` state.
    -   Clears previous timestamps.
-   **`generateTimestamps()`**:
    -   Async function to interact with the Google Generative AI API.
    -   Sets `loading` to true and clears previous `error`.
    -   Initializes `GoogleGenerativeAI` with your API key.
    -   Sends a prompt and the video file URI to the Gemini model.
    -   Parses the text response from the AI:
        -   Splits the response into lines.
        -   Filters lines that match the timestamp format (e.g., `MM:SS - Title` or `HH:MM:SS - Title`).
        -   For each matching line, it extracts the time and title.
        -   Converts the time string into total seconds.
        -   Constructs a YouTube URL with the video ID and the calculated start time in seconds.
        -   Stores the original display text and the generated URL.
    -   Updates the `timestamps` state with the processed data.
    -   Handles potential errors during the API call or parsing.
    -   Sets `loading` to false.
-   **Return (JSX)**:
    -   Renders the main layout with a title.
    -   A form to input the YouTube URL.
    -   An `iframe` to embed the YouTube video player.
    -   A button to trigger `generateTimestamps`.
    -   Displays loading spinner, error messages, or the list of generated timestamps.
    -   Timestamps are rendered as clickable links.

## Customization 🎨

-   **Styling**: Custom styles can be added or modified in `src/App.css`.
-   **AI Prompt**: The prompt sent to the Google Generative AI can be modified in the `generateTimestamps` function to change how timestamps are generated or formatted.
    ```javascript
    const result = await model.generateContent([
      "Please create time-stamps for the video and make sure its in the format of 00:00 - title.", // Modify this prompt
      {
        fileData: {
          fileUri: `https://www.youtube.com/watch?v=${videoId}`,
        },
      },
    ]);
    ```
-   **Timestamp Parsing**: The regular expressions and logic for parsing timestamps in `generateTimestamps` can be adjusted if the AI's output format changes or if a different format is desired.