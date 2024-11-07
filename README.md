# Podcast Summarizer & Highlighter

This project is an AI-based podcast summarizer and highlighter application that uses OpenAI's LLM models to automatically transcribe, summarize, and extract key highlights from podcast episodes. It provides listeners with insightful summaries and highlights of podcast episodes, helping them quickly grasp the main points of each conversation.

---

## Overview

The podcast summarizer application performs a series of tasks that take a podcast episode from raw audio to a digestible summary and structured highlights. This pipeline is ideal for creating weekly newsletters or integrating with a front-end to give users quick access to podcast insights without needing to listen to the entire episode.

The workflow is divided into the following parts:
1. **Download and Transcribe** - Download the latest podcast episode from a specified RSS feed and generate a transcript using OpenAI's Whisper model.
2. **Summarize** - Generate a concise summary that highlights key topics and takeaways.
3. **Extract Speaker Information** - Identify the main guest(s) and provide additional context or background about them.
4. **Highlight Key Moments** - Extract critical insights and questions from the conversation, allowing users to focus on the most engaging parts of the episode.

---

## Features

- **Download Latest Podcast Episode**: Automatically fetches the latest episode from an RSS feed.
- **Transcription**: Uses a speech recognition model to transcribe audio content into text.
- **Summarization**: Provides a concise overview of the episode.
- **Speaker Extraction**: Identifies and retrieves information on the guest(s) using online resources.
- **Highlight Key Moments**: Extracts the most significant and impactful statements or questions from the episode.
- **Generate JSON Output**: Saves all relevant information (title, summary, highlights) to a JSON file for easy retrieval.

---

## Workflow

### Step 1: Podcast Episode Download

1. The `download_podcast_episode` function reads from an RSS feed and downloads the latest podcast episode as an MP3 file.
2. The RSS feed provides metadata like the podcast title, episode title, and image, which are extracted for further use.

```python
def download_podcast_episode(rss_url, local_path="/content/"):
    ...
```

### Step 2: Transcription

The `transcribe_podcast_episode` function uses the Whisper model to transcribe the downloaded MP3 file into a text format. The transcript is then ready for downstream processing.

```python
def transcribe_podcast_episode(episode_path):
    ...
```

### Step 3: Summarization

To give listeners a quick glimpse into the podcast, the `get_podcast_summary` function uses OpenAI's LLM models to summarize the podcast transcript. The summary covers key points and makes the content more accessible for users.

```python
def get_podcast_summary(podcast_transcript):
    ...
```

### Step 4: Speaker Information Extraction

The `get_podcast_speaker` function leverages online sources like Wikipedia to provide background information on the guest(s) featured in the podcast. This additional context helps readers understand the expertise of the guest(s) and the relevance of the conversation.

```python
def get_podcast_speaker(podcast_transcript):
    ...
```

### Step 5: Highlight Extraction

The `get_podcast_highlights` function extracts the top 5 key moments from the episode. These highlights include impactful statements or thought-provoking questions, allowing listeners to focus on crucial insights.

```python
def get_podcast_highlights(podcast_transcript):
    ...
```

### Step 6: Process the Podcast

The `process_podcast` function orchestrates all the above steps to produce a structured output for each podcast episode, saved in a JSON format.

```python
def process_podcast(url):
    ...
```

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your_username/podcast-summarizer.git
   cd podcast-summarizer
   ```

2. Install required libraries:
   ```bash
   pip install -r requirements.txt
   ```

3. Ensure you have an OpenAI API key stored in a secure location, as well as access to Whisper models for transcription.

---

## Usage

1. **Running the Process on a Podcast Feed**:
   ```python
   podcast_feed_url = "https://feeds.megaphone.fm/HS6260485755"
   output = process_podcast(podcast_feed_url)
   ```

2. **Generate a JSON Output**:
   Use the helper function to save the processed podcast details to a JSON file.
   ```python
   import json
   with open("podcast_summary.json", "w") as outfile:
       json.dump(output, outfile)
   ```

3. **Testing the Entire Process**:
   ```python
   # Sample test of the workflow
   process_podcast("https://feeds.megaphone.fm/HS6260485755")
   ```

---

## Extensions

### Ideas for Enhancement

1. **Chapters & Timestamps**: Extract chapter divisions and timestamps for highlights to improve navigation.
2. **UI Integration**: Add a Gradio-based front-end to visualize summaries, highlights, and speaker info.
3. **Support for Multiple Feeds**: Enable processing multiple podcasts at once and save outputs in an organized JSON format.

---

## Example JSON Output

```json
{
    "podcast_title": "The AI Podcast",
    "episode_title": "How AI is Transforming Healthcare",
    "episode_image": "image_url",
    "podcast_summary": "In this episode, we discuss...",
    "podcast_speaker": {
        "name": "Dr. Jane Smith",
        "org": "Healthcare AI Institute",
        "title": "Chief Data Scientist",
        "summary": "Dr. Jane Smith is an expert in AI for healthcare with..."
    },
    "podcast_highlights": [
        "Highlight 1: 'AI has the potential to revolutionize patient care by...' ",
        "Highlight 2: 'One of the main challenges in healthcare AI is...' ",
        ...
    ],
    "podcast_transcription": "The full episode transcript goes here..."
}
```

---

## License

This project is licensed under the [MIT License](LICENSE).
