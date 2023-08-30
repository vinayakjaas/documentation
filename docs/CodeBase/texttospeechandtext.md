---
sidebar_position: 3
---

# Text To Text And Speech Translation

## File Structure
```
project/
├── texttranslation/
│   ├── src/
│   │   ├── lib/
│   │   │   ├── textandspeech.component.ts
│   │   │   ├── textandspeech.module.ts
│   │   │   ├── textandspeech.component.html
│   │   │   ├── textandspeech.service.ts
```

## HTTP Headers:
```
private createHttpHeaders(): HttpHeaders {
    return new HttpHeaders({
      'Content-Type': 'application/json',
      userID: this.config?.userId || '',
      ulcaApiKey: this.config?.apiKey || '',
      Authorization: this.config?.authorizationToken || '',
    });
  }
```
* createHttpHeaders method returns an instance of HttpHeaders with values from the configuration or defaults.

## Translate Text Method:
```
translateText() {
    const text = this.elementRef.nativeElement.querySelector('#textElement').innerText.trim();

    const url = 'https://dhruva-api.bhashini.gov.in/services/inference/pipeline';
    const headers = this.createHttpHeaders();

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
                  source: text,
                },
              ],
            },
          };
```
* The translateText method extracts the text content from an HTML element and sends a translation request to an API.
* It constructs a payload with translation tasks and sends an HTTP POST request.
## Language-related Methods:
```
 getLanguageName(code: string): string {
          const language = this.language.targetLanguageList.find((lang) => lang === code);
          return language ? this.getLanguageDisplayName(language) : '';
        }
      
        getLanguageDisplayName(code: string): string {
          switch (code) {
            case 'sl':
              return 'Select Language';
            case 'as':
              return 'Assamese';
            case 'bn':
              return 'Bengali';
            case 'brx':
              return 'Bodo';
            case 'doi':
              return 'Dogri';
            case 'gom':
              return 'Konkani';
            case 'gu':
              return 'Gujarati';
            case 'hi':
              return 'Hindi';
            case 'kn':
              return 'Kannada';
            case 'ks':
              return 'Kashmiri';
            case 'mai':
              return 'Maithili';
            case 'ml':
              return 'Malayalam';
            case 'mni':
              return 'Manipuri';
            case 'mr':
              return 'Marathi';
            case 'ne':
              return 'Nepali';
            case 'or':
              return 'Odia';
            case 'pa':
              return 'Punjabi';
            case 'sa':
              return 'Sanskrit';
            case 'sat':
              return 'Santali';
            case 'sd':
              return 'Sindhi';
            case 'ta':
              return 'Tamil';
            case 'te':
              return 'Telugu';
            case 'ur':
              return 'Urdu';
            default:
              return '';
          }
        }
```
* getLanguageName and getLanguageDisplayName methods help in converting language codes to human-readable names.
