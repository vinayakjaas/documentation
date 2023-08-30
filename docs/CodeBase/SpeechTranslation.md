---
sidebar_position: 2
---
# TextToSpeech Translation


## File Structure
```
project/
├── texttranslation/
│   ├── src/
│   │   ├── lib/
│   │   │   ├── Speechtranslation.component.ts
│   │   │   ├── Speechtranslation.module.ts
│   │   │   ├── Speechtranslation.component.html
│   │   │   ├── Speechtranslation.service.ts
```
# Component Initialization and Dependencies:
```
import { Component, ContentChild, ElementRef, AfterContentInit ,Inject, Optional } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { SpeechTranslateConfig } from './translate.config';

@Component({
  selector: 'lib-speechtranslate',
  templateUrl: './speechtranslate.component.html',
  styleUrls: ['./speechtranslate.component.css'],
})
```
* The component is defined using the @Component decorator.
* It takes in dependencies through the constructor, mainly the HttpClient and an optional configuration object injected through the @Inject decorator. This configuration object is used to set headers for API requests.

## Text Selection Handling:
```
 onTextSelection(event: MouseEvent) {
    const selectedText = window.getSelection()?.toString().trim();
    this.selectedText = selectedText || ''; // Set selectedText to the actual selected text or an empty string
    this.selectedTargetLanguage = 'sl'; // Reset the selected target language to 'sl' (Select Language) when new text is selected
  }

```
* The onTextSelection method is triggered when a user selects text on the page.
* It uses the window.getSelection() API to get the selected text and assigns it to the selectedText property. It also resets the selectedTargetLanguage to the default value.

## Translation and Speaking Logic:
```
const translationPayload = {
      pipelineTasks: [
        {
          taskType: 'translation',
          config: {
            language: {
              sourceLanguage: this.language.sourceLanguage,
              targetLanguage: this.selectedTargetLanguage,
            },
            serviceId: 'ai4bharat/indictrans-v2-all-gpu--t4',
          },
        },
      ],
      inputData: {
        input: [
          {
            source: this.selectedText,
          },
        ],
      },
    };

```
* The translateAndSpeak method handles the translation and speaking process.
* It constructs a payload for the translation API call and sends an HTTP POST request using Angular's HttpClient.
* If the translation response contains valid output, it sets the translatedOutput property and triggers the speakTranslation method.

## Playing Audio:
```
  playAudio() {
    if (this.ttsOutput) {
      const audioUrl = `data:audio/wav;base64,${this.ttsOutput}`;
      this.audioElement.src = audioUrl;
      this.audioElement.load();
      this.audioElement.play();
    }
  }
```
* The playAudio method plays the TTS-generated audio.
* It creates an audio element and sets its src attribute to the base64-encoded audio content from the API response. Then, it loads and plays the audio element.
