# Recipe to Podcast Converter - Setup Instructions

This application converts food recipes into conversational-style podcasts with customizable duration. Here's how to set it up:

## Prerequisites

- Python 3.8 or higher
- Node.js and npm (if you want to use a JavaScript bundler)
- An OpenAI API key for generating conversational content

## Installation

1. Clone the repository or download the files to your local machine

2. Create a virtual environment and activate it:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use: venv\Scripts\activate
   ```

3. Install required Python packages:
   ```bash
   pip install flask requests beautifulsoup4 openai gtts pydub
   ```

4. Set up your OpenAI API key as an environment variable:
   ```bash
   # On Linux/Mac
   export OPENAI_API_KEY="your-api-key-here"
   
   # On Windows
   set OPENAI_API_KEY=your-api-key-here
   ```

5. Create directories for audio files:
   ```bash
   mkdir -p static/podcasts
   mkdir sounds
   ```

6. For the sound effects feature to work, you'll need to add sound files to the `sounds` directory:
   - chopping.mp3
   - sizzling.mp3
   - mixing.mp3
   - blending.mp3
   - timer.mp3

   You can find free sound effects from sites like Freesound.org or similar resources.

## Running the Application

1. Start the Flask server:
   ```bash
   python app.py
   ```

2. Open your web browser and navigate to:
   ```
   http://127.0.0.1:5000
   ```

## Usage

1. Enter a recipe URL or paste recipe text
2. Adjust the podcast duration using the slider
3. Click "Convert to Podcast"
4. Review the generated script and download it
5. If audio generation is enabled, listen to or download the podcast

## Customization Options

### Text-to-Speech Voices

You can modify the `_text_to_speech` method in the `RecipeToPodcast` class to use different TTS services:

- For more natural-sounding voices, consider using services like:
  - Google Cloud Text-to-Speech
  - Amazon Polly
  - Microsoft Azure Text to Speech
  - Elevenlabs

### LLM Provider

The current implementation uses OpenAI's GPT-4, but you can modify it to use other LLMs:

- Replace the OpenAI implementation in `generate_podcast_script` with your preferred provider
- Adjust the prompt format according to your chosen LLM's requirements

## Troubleshooting

- **Recipe extraction issues**: The current extraction logic works for many recipe sites but might not work for all. Consider enhancing the extraction logic for specific sites you commonly use.
- **API rate limiting**: If you encounter rate limiting with OpenAI, implement request throttling or retries.
- **Audio issues**: If audio generation fails, check if the required libraries (gTTS and pydub) are properly installed, and ensure you have ffmpeg installed on your system.

## Notes on Production Use

For a production environment:
- Add proper error handling and logging
- Implement user authentication if needed
- Set up proper HTTPS with SSL certificates
- Consider containerizing the application with Docker
- Use a production-ready web server like Gunicorn instead of Flask's development server
