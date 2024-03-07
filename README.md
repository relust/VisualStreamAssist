# VisualStreamAssist
Through this project I wanted to add to AlexxIT integration  [StreamAssist](https://github.com/AlexxIT/StreamAssist) personalized and visual responses to be played on an android tablet using the browser mod.

## Pre-requisites

- Home Assistant 2023.11.3 or newer
- A voice assistant [configured in HA](https://my.home-assistant.io/redirect/voice_assistants/) with STT and TTS in a language of your choice
- Install [Browser Mod](https://github.com/thomasloven/hass-browser_mod) integration with HACS. The browser mod media player of android tablet will be used to stream gif files with browser_mod.popup service and audio responses with browser mod media player.
- Install [Rtpmic](https://play.google.com/store/apps/details?id=com.rtpmic&hl=en_US) app on android tablet or or another application to stream mic or camera with sound on tablet. If you use Rtpmic app, on default settings check **auto start streaming** and **start at boot**, **target adress** `255.255.255.255`, **port** `5555`and **audio codec** `G.711a`.
- Optionally install [Fully kiosk browser](https://play.google.com/store/apps/details?id=de.ozerov.fully&hl=en_US) on android tablet and Fully Kiosk Browser integration on Home Assistant.

## Installation

[HACS](https://hacs.xyz/) > Integrations > 3 dots (upper top corner) > Custom repositories > URL: `https://github.com/relust/VisualStreamAssist`, Category: Integration > Add > wait > Stream Assist > Install

### Config Stream Assist

1. Add **Stream Assist** Integration  
   Settings > Integrations > Add Integration > Stream Assist
2. Config **Stream Assist** Integration  
   Settings > Integrations > Stream Assist > Configure

- If you use **Rrpmic**, **Stream URL** is `rtp://192.168.0.xxx:5555`
- On **Player Entity** copy exact name of your **BROWSER MODE PLAYER** of tablet browser (media_player.xxx_xxx).
- On **Browser ID** copy exact name of your **BROWSER MODE BROWSER** (from tablet Browser Mod tab/Browser ID field).
- On **Wake Word detection** use a URL to your MEDIA SOURCE URL. You can simulate a new automation, add action **Media Player**, select **Play media**, select a media player, and from **Pick media** select **Text to speech**, select your language and write a message.
     - **Examples:**
         - `media-source://tts/edge_tts?message=how can I help you&language=en-US-MichelleNeural`
         -  `media-source://tts/google_cloud?message=how can assist you&language=en-GB`
         - `media-source://tts/google_translate?message=yes I am listening you&language=en`  
- Copy [speech.gif and listen.gif](https://github.com/relust/VisualStreamAssist/tree/main/www/voice_assistant) on `www/voice_assistant` directory and on UI **Speech Gif** and **Listen Gif** fields write the path:
     - `/local/voice_assistant/speech.gif`
     - `/local/voice_assistant/listen.gif`
You can select Voice Assistant Pipeline for recognition process: **WAKE => STT => NLP => TTS**. By default componen will use default pipeline. You can create several **Pipelines** with different settings. And several **Stream Assist** components with different settings.

You can select one or multiple Media players (SND) to output audio response. If your camera support two way audio you can use [WebRTC Camera](https://github.com/AlexxIT/WebRTC#stream-to-camera) custom integration to add it as Media player.

You can set STT start media for play "beep" after WAKE detection (ex: `media-source://media_source/local/beep.mp3`).

## Using

Component has MIC switch and multiple sensors - WAKE, STT, INTENT, TTS. There may be fewer sensors, depending on the Pipeline settings.

The sensor attributes contain a lot of useful information about the results of each step of the assistant.

You can also view the pipelines running history in the Home Assistant interface:

- Settings > Voice assistants > Pipeline > 3 dots > Debug
