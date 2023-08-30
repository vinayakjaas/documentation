---
sidebar_position: 1
---

# TextTranslation

## File Structure
```
project/
├── texttranslation/
│   ├── src/
│   │   ├── lib/
│   │   │   ├── texttranslation.component.ts
│   │   │   ├── texttranslation.module.ts
│   │   │   ├── texttranslation.component.html
│   │   │   ├── text-translation.service.ts
```

## Class Properties:
```
@ContentChild('contentElement') contentElementRef?: ElementRef;
language: Language = { /* ... */ };
selectedTargetLanguage: string = 'sl';
translatedOutput: string | undefined;
showTranslation: boolean = false;
showContentElement: boolean = true;
```
@ContentChild('contentElement') contentElementRef?: ElementRef;: This decorator is used to access a content projection named 'contentElement'. The contentElementRef will hold a reference to the projected content's element.

## Constructor:
```
constructor(
  private http: HttpClient,
  @Optional() @Inject('TEXT_TRANSLATE_CONFIG') private config: TextTranslateConfig
) {}
```
The constructor injects HttpClient for making HTTP requests and the optional TextTranslateConfig for configuration.

## Translation Logic:
```
translateContent() {
  // ...
  this.http.post<ApiResponse>(url, payload, { headers }).subscribe(
    (response) => {
      // ...
    },
    (error) => {
      // ...
    }
  );
}
```
This method handles the translation process using an HTTP POST request. It sends the input text to an API endpoint and processes the response.

# Toggle Translation and Content Methods:
```
toggleTranslation() {
  this.showTranslation = !this.showTranslation;
}

getContent(): string {
  return this.contentElementRef?.nativeElement.innerText.trim() || '';
}
```
toggleTranslation method toggles the showTranslation boolean.

getContent method extracts the text content from the projected element.