# VisualStreamAssist
Through this project I wanted to add to the integration of AlexxIT [StreamAssist](https://github.com/AlexxIT/StreamAssist) personalized and visual responses to be played on an android tablet using the browser mod.

## Pre-requisites

- Home Assistant 2023.11.3 or newer
- A voice assistant [configured in HA](https://my.home-assistant.io/redirect/voice_assistants/) with STT and TTS in a language of your choice
- Install Browser Mod integration with HACS. The browser mod media player of android tablet will be used to stream gif files with browser_mod.popup service and audio responses with browser mod media player
- Optionally install Fully kiosk browser on android tablet and Fully Kiosk Browser integration on Home Assistant.

## Installation

[HACS](https://hacs.xyz/) > Integrations > 3 dots (upper top corner) > Custom repositories > URL: `https://github.com/relust/VisualStreamAssist`, Category: Integration > Add > wait > Stream Assist > Install

### Config Stream Assist

1. Add **Stream Assist** Integration  
   Settings > Integrations > Add Integration > Stream Assist
2. Config **Stream Assist** Integration  
   Settings > Integrations > Stream Assist > Configure

You can select or camera entity_id as audio (MIC) source or stream URL.

You can select Voice Assistant Pipeline for recognition process: **WAKE => STT => NLP => TTS**. By default componen will use default pipeline. You can create several **Pipelines** with different settings. And several **Stream Assist** components with different settings.

You can select one or multiple Media players (SND) to output audio response. If your camera support two way audio you can use [WebRTC Camera](https://github.com/AlexxIT/WebRTC#stream-to-camera) custom integration to add it as Media player.

You can set STT start media for play "beep" after WAKE detection (ex: `media-source://media_source/local/beep.mp3`).

## Using

Component has MIC switch and multiple sensors - WAKE, STT, INTENT, TTS. There may be fewer sensors, depending on the Pipeline settings.

The sensor attributes contain a lot of useful information about the results of each step of the assistant.

You can also view the pipelines running history in the Home Assistant interface:

- Settings > Voice assistants > Pipeline > 3 dots > Debug
