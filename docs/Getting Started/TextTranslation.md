---
sidebar_position: 1
---

# TextTranslation
Bhashini-Translation is a powerful language translation library designed specifically for Indian languages. It harnesses the power of AI to offer accurate and efficient translation services. With Bhashini-Translation, you can easily integrate advanced language translation capabilities into your web applicationsIt's integrating with [Bhashini Api](https://bhashini.gitbook.io/bhashini-apis/). It seamlessly integrates with web frontends such as Vanilla JS, React, and Angular.  
Bhashini follows [ISO-639 series](https://www.loc.gov/standards/iso639-2/php/code_list.php) of language codes.

Users interact with the Text-to-Text Translation tool through a user interface, which can be a web-based application, a desktop program, or a mobile app. The interface typically includes text input fields where users can type or paste the source text they want to translate. Additionally, users can select their preferred target language from a list of available languages.

# Getting Started
1. Install the package using npm or yarn
```bash
npm install bashaini-texttranslation 
```

```shell
yarn add bashaini-texttranslation  
```
2. Import the package in Module
```shell
import { TextTranslationModule } from 'bhashini-texttranslation';
import { TextTranslateConfig } from 'bhashini-texttranslation/lib/text-translate.config';
```
3.Add Your userId,apiKey,authorizationToken For configuration
```
providers: [
    {
      provide: 'TEXT_TRANSLATE_CONFIG', // Use a string token to provide the configuration
      useValue: {
        userId: 'Your User Id', // Provide the user ID here
        apiKey: 'Your apiKey', // Provide the API key here
        authorizationToken: 'Your authorizationToken', // Provide the authorization token here
      } as SpeechTranslateConfig,
    },
]
```
4 Call Library  
```
<lib-text-translation></lib-text-translation>
```
## get authentication details
Signup[here](https://bhashini.gov.in/ulca/user/register) to get authentication details  
   - Step 1: Fill out the registration form.
   - Step 2: Perform email authentication to enable login functionality
   - Step 3: Login using the authenticated email.
   - Step 4: Open the "My Profile" section
   - Step 5: create the API Key using Generate Button under My Profile section.   
   - Step 6: press generate in api key to get credentials
   - Step 7: now copy `userid`, `UlcaApiKey`, and 	`authorizationToken` for `Meity` and pass as argument in `bhashini.auth("userid", "UlcaApiKey", "authorizationToken")` function 
