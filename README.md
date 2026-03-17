# AI-Powered README Generator for GitHub Repositories

## Description
This project provides an automated solution for generating comprehensive and professional `README.md` files for any given GitHub repository. Leveraging Google's advanced Gemini generative AI models, it intelligently processes the repository's source code, understands its structure, technologies, and purpose. It employs a Retrieval Augmented Generation (RAG) approach to effectively chunk and prioritize code segments, which are then fed as context to the LLM to produce an accurate, detailed, and well-structured `README.md` complete with sections like Description, Tech Stack, Installation, Usage, and more. This tool aims to streamline documentation efforts for developers by reducing manual `README` writing.

## Tech Stack
*   **Languages**: Python
*   **Generative AI**: Google Gemini API (specifically `gemini-2.5-flash`)
*   **Core Libraries**:
    *   `google-generativeai`: Python client for interacting with Google's GenAI models.
    *   `python-dotenv`: For loading environment variables from a `.env` file.
*   **Architectural Principles**: Retrieval Augmented Generation (RAG) for source code processing and context creation.

## Project Structure
The repository is organized into several Python modules, each handling a specific part of the README generation pipeline:

```
.
├── .env                  # Environment variables (e.g., GEMINI_API_KEY)
├── generate_readme.py    # Main script to orchestrate README generation
├── init_models.py        # Initializes the Google Gemini client
├── rag_chunker.py        # Handles repository file reading, chunking, and context building
├── readme_generator.py   # Defines the LLM prompt and calls the Gemini model
└── README.md             # The generated README file (output of this project)
```

*   `generate_readme.py`: This is the entry point of the application. It orchestrates the process of reading the repository, building context, calling the `ReadmeGenerator`, and saving the output.
*   `rag_chunker.py`: Contains the `RAGChunker` class, which is responsible for scanning a given directory, filtering code files based on extensions and excluded folders, splitting file content into manageable chunks with overlap, and prioritizing important files (e.g., `main.py`, `requirements.txt`) to ensure they are included in the LLM context.
*   `init_models.py`: Provides the `init_models` class, which handles the secure loading of API keys from `.env` and initializes the Google Gemini client. It encapsulates the logic for making API calls to the Gemini generative models.
*   `readme_generator.py`: Contains the `ReadmeGenerator` class. It defines the comprehensive prompt template used to instruct the Gemini model on how to generate a professional `README.md`. This class formats the source code context and repository structure before sending it to the LLM and processes the raw LLM output.

## Installation
To set up and run this README generator, follow these steps:

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/annu0603/Flood-Prediction-Using-Satellite-Images.git
    cd Flood-Prediction-Using-Satellite-Images
    ```

2.  **Create and activate a virtual environment**:
    It's recommended to use a virtual environment to manage dependencies.
    ```bash
    python -m venv venv
    # On macOS/Linux
    source venv/bin/activate
    # On Windows
    venv\Scripts\activate
    ```

3.  **Install dependencies**:
    Install the required Python packages.
    ```bash
    pip install google-generativeai python-dotenv
    ```

4.  **Obtain a Google Gemini API Key**:
    You will need an API key for Google Gemini. You can obtain one from the [Google AI Studio](https://makersuite.google.com/app/apikey).

## Usage
Once installed and configured, you can run the `generate_readme.py` script to create a `README.md` for the current repository.

1.  **Configure your API Key**:
    Create a `.env` file in the root of the project directory (where `generate_readme.py` is located) and add your Gemini API key:
    ```dotenv
    GEMINI_API_KEY="YOUR_GEMINI_API_KEY_HERE"
    ```
    (See the Configuration section for more details on `.env` variables).

2.  **Run the generator**:
    Execute the main script from your terminal:
    ```bash
    python generate_readme.py
    ```
    This command will analyze the code in the current directory and generate a `README.md` file (or update an existing one) in the same directory. The console will show progress messages during the generation process.

## Configuration
The project uses environment variables managed by `python-dotenv` for sensitive information and customizable settings.

*   `.env` file:
    Create a file named `.env` in the root directory of the project.

    *   `GEMINI_API_KEY`: **Required**. Your API key for authenticating with the Google Gemini API.
        ```dotenv
        GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
        ```

    *   `GITHUB_REPOSITORY`: **Optional**. This variable allows you to explicitly set the repository name (e.g., `your-username/your-repo`) that will be used in the README title and GitHub URL. If not set, the script defaults to `"your-username/your-repo"`. For documentation of *this* project, it will derive it.
        ```dotenv
        # Example if you want to override the repo name for the README being generated
        # GITHUB_REPOSITORY="my-organization/my-cool-project"
        ```

## Contributing
Contributions are welcome! If you have suggestions for improvements, new features, or bug fixes, please feel free to:

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Commit your changes.
4.  Push your branch to your fork.
5.  Open a Pull Request with a clear description of your changes.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.