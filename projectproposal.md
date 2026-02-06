# Project Proposal

## 1. System Overview

**System Name**
L.U.M.I (Logical Utility Machine Intelligence)

**Problem Statement**
Modern AI assistants (like Alexa, Siri, or Copilot) rely heavily on cloud processing, which raises significant privacy concerns, introduces latency, and requires a constant internet connection. Users often lack a unified, offline-capable interface that integrates powerful Large Language Models (LLMs) deeply with their local desktop environment without sending sensitive voice, usage, or query data to third-party servers.

**Target Users**
*   **Privacy-Conscious Users:** Individuals who want AI assistance without data tracking.
*   **Developers & Power Users:** Those interested in running local LLMs (Ollama) and customizing their assistant.
*   **Windows Users:** People seeking a native, aesthetically pleasing assistant that matches the Windows 11 Fluent Design and helps manage productivity.

## 2. Component Breakdown

| Component | Description |
| :--- | :--- |
| **Desktop App Component** | A native Windows GUI application built with Python and Qt (PyQt-Fluent-Widgets). It serves as the central hub for voice interaction, chat, system monitoring, and personal organization. |
| **Integrative Technology Component (ML)** | **ML:** Local LLM inference via Ollama, Speech-to-Text (Whisper), and Text-to-Speech (Piper). |
| **Backend Logic Component** | A local Python core that manages state, routes user intents (using a lightweight router model), and orchestrates communication between the GUI and the Ollama API. |

*(Note: A dedicated Mobile App component is not part of the initial scope as this is a desktop-centric utility, but the architecture allows for future expansion.)*

## 3. Frontend Feature List

### Desktop App Features (Admin / User-Facing)

**Voice & Chat Interface**
– **Wake Word Detection:** continuously listens for the "Lumi" wake word to initiate hands-free interaction.
– **Streaming Chat:** Displays AI responses token-by-token in real-time for a responsive feel.
– **Voice Commands:** Allows natural language control of PC functions and productivity tools.

**Dashboard & System Monitor**
– **System Stats:** Real-time visualization of CPU and RAM usage in the title bar or dashboard.
– **Daily Briefing:** Displays AI-curated news summaries (Tech, Science, Top Stories) and calendar events.
– **Weather Widget:** Shows current conditions and forecasts based on user location.

**Productivity Tools**
– **Planner/Calendar:** Interface to view and manage upcoming events.
– **Timer & Alarm:** Set and view countdown timers and alarms.

**Settings & Configuration**
– **Model Selection:** Dropdown to switch between installed LLMs (e.g., Qwen, DeepSeek).
– **Customization:** Options to adjust wake word sensitivity, target frame rate, and weather location.

---

### *Integrative Features (ML Specifics)*

**ML-Driven Features**
– **Intent Recognition:** Uses a local router model to classify prompts (e.g., distinguishing a "search" request from a "chat" request).
– **Local Search:** Ability to search the web and summarize results using the local LLM.
– **Personal Assistance:** Context-aware responses based on user queries and system status.

## 4. Integrative Technology Details

**Chosen Technologies:**
1.  **Machine Learning (ML):** Ollama (LLM Server), Whisper (STT), Piper (TTS), and a custom classification router.

**Description of Integration:**
The system runs a local **Ollama** server instance in the background to handle heavy inference tasks (chat generation). When the user speaks, **RealTimeSTT** (using Whisper) transcribes audio to text. This text is passed to a lightweight **Router Model** (ML) which decides if the user wants to chat or perform a system task.
*   The prompt is sent to Ollama, and the streaming response is displayed in the GUI while being read aloud by **Piper TTS**.
*   The system uses local processing for all voice and text data, ensuring complete privacy.

## 5. Primary Screen for Week 1 Implementation

**Selected Screen Name**
The Main Dashboard (Home Interface)

**Purpose of this screen**
To serve as the landing page that greets the user, providing immediate value (weather, system stats) and a clear entry point for interaction (chat input/microphone status).

**Key UI elements to be displayed**
*   **Navigation Sidebar:** For switching between Home, Chat, and Settings.
*   **Greeting Banner:** "Good Morning/Afternoon" with current time/date.
*   **System Monitor:** Progress rings or bars showing CPU/Memory load.
*   **Weather Card:** Icon and temperature for the configured location.
*   **Chat Input Area:** Text box and Microphone button for issuing commands.

## 6. Notes for Frontend Development

**Assumptions & Design Considerations:**
*   **Fluent Design:** The UI must strictly adhere to Windows 11 Fluent Design principles (Mica effects, rounded corners, Acrylic transparency) using `QMateriaWidgets` or `QFluentWidgets`.
*   **Performance:** The GUI must run on a separate thread from the heavy ML inference loops to remain responsive (no freezing while the AI thinks).
*   **Dark Mode:** The application should default to or support a high-contrast dark mode as shown in the project screenshots.
*   **Screen Space:** The dashboard should be clean and not cluttered; detailed interactions (like long chats) should happen in their specific tabs.
