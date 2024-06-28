# quiz-app-streamlit-chromadb-langchain-langchain-google-vertexai-pypdf

Welcome to QuizApp! This project is designed to create AI-powered quizzes using Google Cloud, Vertex AI, and ChromaDB. Follow the detailed steps below to set up and run the project on your local machine.

## Task 1: Google Cloud, Vertex AI, & SDK Authentication
**Description:** Get started on Google Cloud for AI projects. Follow these steps to create an account, set up a project, enable Vertex AI APIs, and manage service accounts with owner permissions.

### Steps:
1. Create a Google Cloud account and set it up on your desktop.

## Task 2: Dev Environment Setup
**Description:** Set up the development environment for Mission Quizzify. Learn to clone, fork, and manage security for a GitHub repository. Set up service account keys and handle authentication errors.

### Steps:
1. Clone the repository:
    ```bash
    git clone https://github.com/radicalxdev/mission-quizify.git
    ```
2. Navigate to the project directory:
    ```bash
    cd .\mission-quizify\
    ```
3. Create a virtual environment:
    ```bash
    python -m venv env
    ```
4. Activate the virtual environment:
    ```bash
    env\Scripts\activate
    ```
5. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

## Task 3: Document Ingestion
**Description:** Create a file uploader, process PDFs using PyPDFLoader, and test document ingestion.

### Steps:
1. Install the required package:
    ```bash
    pip install langchain_community
    ```
2. Use the Streamlit file uploader widget to allow users to upload PDF files.
    - Use `st.file_uploader()` with the 'type' parameter set to 'pdf'.
3. For each uploaded PDF file:
    - Generate a unique identifier and append it to the original file name before saving it temporarily.
    - Use Langchain's PyPDFLoader on the path of the temporary file to extract pages.
    - Clean up by deleting the temporary file after processing.
4. Keep track of the total number of pages extracted from all uploaded documents.

## Task 4: Embedding with Vertex AI & Langchain
**Description:** Implement the `__init__` method, initialize `VertexAIEmbeddings`, and test by embedding 'Hello World' in Streamlit.

### Steps:
1. Implement the `__init__` method to accept 'model_name', 'project', and 'location' parameters.
2. Initialize the `self.client` attribute as an instance of `VertexAIEmbeddings` using the provided parameters.

## Task 5: Data Pipeline to Chroma DB
**Description:** Process documents, split text chunks using `CharacterTextSplitter`, and create a Chroma collection in memory. Test integration with a small PDF using Streamlit.

### Steps:
1. Check if any documents have been processed by the `DocumentProcessor` instance. If not, display an error message using Streamlit's error widget.
2. Split the processed documents into text chunks suitable for embedding and indexing using `CharacterTextSplitter`.
    - Define a separator, chunk size, and chunk overlap.
3. Create a Chroma collection in memory with the text chunks obtained from step 2 and the embeddings model initialized in the class. Use the `Chroma.from_documents` method for this purpose.

## Task 6: Streamlit UI for Data Ingestion
**Description:** Initialize `DocumentProcessor`, `EmbeddingClient`, and `ChromaCollectionCreator`, then use Streamlit to build a user-friendly form for topic selection and question quantity. Use the Chroma collection for quiz question generation.

### Steps:
1. Initialize an instance of the `DocumentProcessor` and invoke the `ingest_documents()` method to process the uploaded PDF documents.
2. Configure and initialize the `EmbeddingClient` with the specified model, project, and location details.
3. Instantiate the `ChromaCollectionCreator` using the previously initialized `DocumentProcessor` and `EmbeddingClient`.
4. Use Streamlit to construct a form for topic input and question quantity selection.
5. After form submission, use the `ChromaCollectionCreator` to create a Chroma collection from the processed documents.
6. Allow users to input a query relevant to the quiz topic and use the generated Chroma collection to extract information for quiz question generation.

## Task 7: Quiz Generator Class
**Description:** Set up the `QuizGenerator` to use the "gemini-pro" model, configure parameters for controlled output, and integrate with vectorstore for context-driven question generation.

### Steps:
1. Set the LLM's model name to "gemini-pro".
2. Configure the 'temperature' parameter to control the randomness of the output.
3. Specify 'max_output_tokens' to limit the length of the generated text.
4. Initialize the LLM with the specified parameters for generating quiz questions.

## Task 8: Generate Quiz Algorithm
**Description:** Generate a quiz by looping through questions, ensuring uniqueness with a retry limit, and validating against the question bank. Test with Streamlit.

### Steps:
1. Generate a question based on the provided topic and context.
2. Provide 4 multiple choice answers to the question as a list of key-value pairs.
3. Specify the correct answer from the list of answers.
4. Provide an explanation for why the answer is correct.

## Task 9: Generate Quiz UI
**Description:** Implement the `QuizManager` class to store and manage quiz questions, allowing movement between questions. Use Streamlit to display questions and test the application with PDF ingestion.

### Steps:
1. Store the provided list of quiz question objects in an instance variable named `questions`.
2. Calculate and store the total number of questions in the list in an instance variable named `total_questions`.

## Task 10: Screen State Handling
**Description:** Initialize the question bank, set topic and question quantity with Streamlit widgets, and manage quiz generation and display. Test the application for a seamless user experience.

### Steps:
1. Initialize the question bank list in `st.session_state`.
2. Set topic input and number of questions.
3. Initialize a `QuizGenerator` class using the topic, number of questions, and the Chroma collection.
4. Initialize the question bank list in `st.session_state`.
5. Set a `display_quiz` flag in `st.session_state` to True.
6. Set the `question_index` to 0 in `st.session_state`.
7. Set `index_question` using the `QuizManager` method `get_question_at_index` passing the `st.session_state["question_index"]`.
8. Use Streamlit to navigate to the next and previous questions.
