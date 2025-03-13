### **NebulaBot: A Langchain Multi-Role Chatbot**

---

## **Overview**

**NebulaBot** is a web-based application that allows users to interact with prebuilt or custom roles or characters. Each character has a unique personality, backstory, and conversation style, powered by Google's Gemini LLM. The app is built using **Streamlit** for the frontend, **LangChain** for integrating the LLM, and **SQLite** for storing prebuilt character data.

---

## **Technologies Used**

### **1. Streamlit**
- **Purpose**: Frontend framework for building the web interface.
- **Version**: `1.32.0`
- **Features**:
  - Real-time chat interface with `st.chat_input` and `st.chat_message`.
  - Sidebar for character creation and selection.
  - Session state management for persistent data.

### **2. LangChain**
- **Purpose**: Framework for integrating and managing interactions with the Gemini LLM.
- **Version**: `langchain-google-genai==0.0.11`
- **Features**:
  - Integration with Google's Gemini LLM for generating character responses.
  - Prompt templating for maintaining character personality and context.

### **3. Google Gemini LLM**
- **Purpose**: Large Language Model for generating conversational responses.
- **Model**: `gemini-2.0-flash-lite`
- **Features**:
  - High-quality, context-aware responses.
  - Customizable temperature for controlling creativity.

### **4. SQLite**
- **Purpose**: Lightweight database for storing prebuilt character data.
- **Version**: `sqlite3==2.6.0`
- **Features**:
  - Local database for storing character details (name, personality, backstory, etc.).
  - Read-only access for prebuilt characters.

### **5. Python Dotenv**
- **Purpose**: Load environment variables (e.g., API keys) from a `.env` file.
- **Version**: `python-dotenv==1.0.0`
- **Features**:
  - Securely manage sensitive data like the `GOOGLE_API_KEY`.

---

## **APIs Used**

### **1. Google Generative AI API**
- **Endpoint**: Integrated via LangChain's `ChatGoogleGenerativeAI`.
- **Purpose**: Generate conversational responses based on character prompts.
- **Authentication**: Requires a `GOOGLE_API_KEY` stored in the `.env` file.

---

## **Project Structure**

```
character-chatbot/
├── app.py                  # Main application file
├── initialize_database.py  # Script to initialize the SQLite database
├── prebuilt_characters.db  # SQLite database for prebuilt characters
├── .env                   # Environment variables (e.g., GOOGLE_API_KEY)
├── requirements.txt        # Python dependencies
```

---

## **Setup Instructions**

### **1. Prerequisites**
- Python 3.8 or higher.
- A Google API key for Gemini LLM access.

### **2. Install Dependencies**
1. Clone the repository:
   ```bash
   git clone https://github.com/PriyanujBoruah/NebulaBot.git
   cd character-chatbot
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```

3. Activate the virtual environment:
   - On Windows:
     ```bash
     venv\Scripts\activate
     ```
   - On macOS/Linux:
     ```bash
     source venv/bin/activate
     ```

4. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### **3. Set Up Environment Variables**
1. Create a `.env` file in the project root:
   ```env
   GOOGLE_API_KEY=your_google_api_key_here
   ```

2. Replace `your_google_api_key_here` with your actual Google API key.

### **4. Initialize the Database**
1. Run the `initialize_database.py` script to create the SQLite database and populate it with prebuilt characters:
   ```bash
   python initialize_database.py
   ```

### **5. Run the Application**
1. Start the Streamlit app:
   ```bash
   streamlit run app.py
   ```

2. Open the app in your browser (usually at `http://localhost:8501`).

---

## **How to Use the Chatbot**

### **1. Select a Character**
- Use the sidebar to browse characters by category (e.g., Assistants, Anime, Entertainment & Gaming).
- Click **Select Character** to start chatting.

### **2. Create a Custom Character**
- Expand the **Create New Character** section in the sidebar.
- Fill in the character's name, personality, backstory, and example dialogues.
- Click **Create Character** to add the character to the list.

### **3. Chat with a Character**
- Type your message in the chat input box at the bottom of the screen.
- The character will respond based on their personality and backstory.

### **4. View Conversation History**
- All conversations are saved in the session state.
- Scroll up to view previous messages.

---

## **Code Walkthrough**

### **1. `app.py`**
- **Main Application**:
  - Initializes the Streamlit app and session state.
  - Loads prebuilt characters from the SQLite database.
  - Provides UI for character creation, selection, and chatting.

### **2. `initialize_database.py`**
- **Database Initialization**:
  - Creates the `prebuilt_characters.db` SQLite database.
  - Populates the database with prebuilt characters.

### **3. `prebuilt_characters.db`**
- **Database**:
  - Stores character details (name, personality, backstory, examples, category).
  - Used as a read-only data source for prebuilt characters.

---

## **Customization**

### **1. Add More Characters**
- Modify `initialize_database.py` to include additional prebuilt characters.
- Example:
  ```python
  preset_characters = [
      {
          "name": "New Character",
          "personality": "Friendly and helpful",
          "backstory": "A new character with a unique story.",
          "examples": "None",
          "category": "Assistants"
      }
  ]
  ```

### **2. Change the LLM Model**
- Update the `model` parameter in `app.py`:
  ```python
  llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash-lite", temperature=0.7)
  ```

### **3. Modify the Prompt Template**
- Edit the `prompt_template` in `app.py` to customize the character's response style:
  ```python
  prompt_template = PromptTemplate.from_template(
      """You are {name}, a character with these personality traits: {personality}.
  Backstory: {backstory}
  Example dialogues: {examples}

  Previous conversation:
  {history}

  Stay in character and respond to this message:
  User: {input}
  {name}:"""
  )
  ```

---

## **Troubleshooting**

### **1. Missing API Key**
- Ensure the `.env` file contains the `GOOGLE_API_KEY`.
- Example:
  ```env
  GOOGLE_API_KEY=your_api_key_here
  ```

### **2. Database Not Found**
- Run `initialize_database.py` to create the SQLite database.

### **3. Dependency Issues**
- Reinstall dependencies using:
  ```bash
  pip install -r requirements.txt
  ```

---

## **Conclusion**

The **Character Chatbot** is a versatile and interactive application that leverages modern AI and web technologies to provide a unique conversational experience. With its modular design and extensible architecture, it can be easily customized and expanded for various use cases.
