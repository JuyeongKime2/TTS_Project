"# TTS_Project" 
AI Voice Data Processing (AI 서인국)
This project provides a comprehensive workflow for extracting audio data from YouTube videos and performing voice recognition and synthesis. The project demonstrates using tools like yt-dlp, OpenAI's Whisper, and text-to-speech (TTS) APIs to create a voice model, inspired by the voice of a specific individual (e.g., "AI 서인국"). This README provides an overview of the code and how to use it effectively.

이 프로젝트는 YouTube 동영상에서 오디오 데이터를 추출하고 음성 인식 및 합성을 수행하는 일련의 과정을 제공합니다. yt-dlp, OpenAI의 Whisper, TTS (Text-to-Speech) API와 같은 도구를 사용하여 특정 인물(예: "AI 서인국")의 목소리를 모델링하는 방법을 보여줍니다. 이 README는 코드의 개요와 사용 방법을 안내합니다.

Table of Contents / 목차
Requirements / 요구 사항
Installation / 설치
Usage / 사용 방법
1. Extracting Audio from YouTube / 유튜브에서 오디오 추출하기
2. Transcribing Audio with Whisper / Whisper를 사용하여 음성 텍스트 변환
3. Text-to-Speech Synthesis / 텍스트 음성 합성
References / 참고 자료
Requirements / 요구 사항
Python 3.x

yt-dlp

whisper by OpenAI

ffmpeg

Additional Python libraries as specified in the code (e.g., scipy, TTS)

Python 3.x

yt-dlp

OpenAI의 whisper

ffmpeg

코드에서 요구하는 추가적인 Python 라이브러리 (scipy, TTS 등)

------------------------------------------------------------------------------------------------------------------------
Installation / 설치
To set up the required environment, use the following commands:

필요한 환경을 설정하려면 아래 명령어를 사용하세요:


# Install yt-dlp for downloading audio from YouTube
# 유튜브에서 오디오를 다운로드하기 위한 yt-dlp 설치
pip install yt_dlp

# Install OpenAI's Whisper
# OpenAI의 Whisper 설치
pip install git+https://github.com/openai/whisper.git

# Install other required libraries
# 추가적으로 필요한 라이브러리 설치
pip install scipy
pip install TTS

---------------------------------------------------------------------------------------------------------------------------------
Usage / 사용 방법
1. Extracting Audio from YouTube / 유튜브에서 오디오 추출하기
This project uses yt-dlp to extract audio from a YouTube video. You can download the audio in the best quality and convert it to .mp3.

이 프로젝트는 yt-dlp를 사용하여 유튜브 동영상에서 오디오를 추출합니다. 최고 품질의 오디오를 다운로드하고 .mp3로 변환할 수 있습니다.

----------------------------------------------------------------------------------------------------------------------------------
Example code to download audio / 오디오 다운로드를 위한 예시 코드:

import yt_dlp

# YouTube video URL
# 유튜브 비디오 URL
video_url = 'https://www.youtube.com/watch?v=YzTQLsD5DHg'

# Download and convert options
# 다운로드 및 변환 옵션
ydl_opts = {
    'format': 'bestaudio/best',  # Download the best audio quality / 최고 품질의 오디오 다운로드
    'postprocessors': [{  # Convert to mp3 / mp3로 변환
        'key': 'FFmpegExtractAudio',
        'preferredcodec': 'mp3',
        'preferredquality': '192',
    }],
    'outtmpl': 'youtube_output',  # Output filename / 출력 파일명
}

# Execute yt-dlp
# yt-dlp 실행
with yt_dlp.YoutubeDL(ydl_opts) as ydl:
    ydl.download([video_url])
2. Transcribing Audio with Whisper / Whisper를 사용하여 음성 텍스트 변환
Use OpenAI's Whisper model to transcribe the downloaded audio. Whisper is a powerful ASR (Automatic Speech Recognition) model that can handle various languages and accents.

OpenAI의 Whisper 모델을 사용하여 다운로드된 오디오를 텍스트로 변환합니다. Whisper는 다양한 언어와 억양을 처리할 수 있는 강력한 자동 음성 인식(ASR) 모델입니다.

---------------------------------------------------------------------------------------------------------------------------------
Example code to transcribe audio (replace with your audio file path) / 오디오를 텍스트로 변환하는 예시 코드 (사용할 오디오 파일 경로로 변경하세요):

import whisper

model = whisper.load_model("small")
result = model.transcribe("youtube_output.mp3")
print(result['text'])
3. Text-to-Speech Synthesis / 텍스트 음성 합성
Use a TTS (Text-to-Speech) model to convert text into synthesized speech. This project uses a multilingual TTS model to create a synthesized voice.

TTS (Text-to-Speech) 모델을 사용하여 텍스트를 합성된 음성으로 변환합니다. 이 프로젝트에서는 다국어 TTS 모델을 사용하여 합성 음성을 생성합니다.

---------------------------------------------------------------------------------------------------------------------------------
Example code for TTS synthesis / TTS 합성을 위한 예시 코드:

from TTS.api import TTS

tts = TTS(model_name="tts_models/multilingual/multi-dataset/xtts_v2", gpu=True)
tts.tts_to_file(text='서인국이 간다!', file_path='./output.wav', speaker_wav='/path/to/speaker.wav', language='ko')

---------------------------------------------------------------------------------------------------------------------------------
Notes / 참고 사항
Ensure ffmpeg is installed on your system for audio processing.

For more natural voice synthesis, provide a high-quality audio sample of the target voice in the speaker_wav parameter.

오디오 처리를 위해 시스템에 ffmpeg가 설치되어 있는지 확인하세요.

보다 자연스러운 음성 합성을 위해 speaker_wav 파라미터에 대상 목소리의 고품질 오디오 샘플을 제공하세요.

---------------------------------------------------------------------------------------------------------------------------------
References / 참고 자료
yt-dlp: GitHub Repository
OpenAI's Whisper: GitHub Repository
TTS (Text-to-Speech) Library: GitHub Repository
