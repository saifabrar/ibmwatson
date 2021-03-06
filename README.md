# Evangelizing [IBM Watson](https://www.ibm.com/watson "Watson Homepage")

IBM Watson is an enterprise A.I. platform, named after IBM's first CEO Thomas J. Watson (1874-1956).

Watson came to highlight after winning $1 million in quiz tournament Jeopardy! of 2011, against legendary champions Brad Rutter and Ken Jennings.

<details>
  
  <summary>Table of Contents</summary>
  * [References](#references-about-ibm-watson)
  * [Services provided by IBM Watson](#services-provided-by-ibm-watson)
    * [Sub-level](#sublevel)
  * [Services within WDC](#services-within-wdc)
  * [Tutorial](#tutorial)
  * [Watson Services](#watson-services)
  * [Authentication Tokens](#authentication-tokens)
  * [Documentation](#documentation)
  * [Questions](#questions)
  * [Open Source @ IBM](#open-source--ibm)
  * [IBM Watson usage across the world](#ibm-watson-usage-across-the-world)
</details>

## References about IBM Watson
- [Wikipedia](https://en.wikipedia.org/wiki/Watson_(computer))
- [YouTube channel](https://www.youtube.com/user/IBMWatsonSolutions)
- [StackOverflow](https://stackoverflow.com/questions/tagged/ibm-watson)
- [GitHub](https://github.com/IBM-Watson)

## Solutions provided by IBM Watson
Watson provides solutions to manage the full AI lifecycle, from preparing the data, building the AI models, and deploying into production.
- Watson Studio
- Watson Machine Learning
- Watson OpenScale
- Watson Knowledge Catalog
- Watson Developer Cloud (WDC) *<-- we are going to use this*

## Services within WDC
IBM Watson Developer Cloud(WDC) provides a collection of REST API's and SDK's to integrate AI into your applications!  
Following services are provided by WDC:
- Assistant
- Discovery
- Language Translator V3
- Natural Language Classifier
- Natural Language Understanding
- Language Translator
- Personality Insights
- Speech to Text
- Text to Speech
- Tone Analyzer
- Visual Recognition


## SDK's provided by WDC
Each SDK is a client library to quickly get started with the various WDC services.  
The SDK's are available for the following languages:
- Python
- Java
- Swift
- Dotnet
- Node.js
- Unity (enables [Unity 3D applications](https://unity3d.com/get-unity) to be powered by Watson)

# Tutorial
Here's everything you need to start building with Watson.

## Prerequisites
1. Create free account on [IBM Cloud](https://cloud.ibm.com/)
1. Install WDC SDK for the language of your choice, e.g. [Python SDK](https://github.com/watson-developer-cloud/python-sdk)
```
pip install --upgrade ibm-watson
```
Versions prior to 3.0.0 can be installed using:
```
pip install --upgrade watson-developer-cloud
```
1. cURL : Pre-installed in Linux; download [curl for Windows](https://curl.haxx.se/download.html)
1. Basics of Python
1. Basics of RESTful API's
1. Basics of JSON

## Creating AI service
1. Login to the [IBM Cloud]( https://cloud.ibm.com/)
1. Check various resources in the [Catalog](https://cloud.ibm.com/catalog)
1. Click on **AI** in the left pane to see all AI services.
1. Select an AI service of interest, e.g. [language translator](https://cloud.ibm.com/catalog/services/language-translator)
1. Study various information about the selected service, like **'Features', 'Pricing Plans'**, etc.
1. Click **'Create'** at the botton of the page
1. Click **'Manage'** in the left pane.
1. Click **'Show Credentials'** to view your credentials, i.e. API-key and URL.
1. Copy the `API Key` and `URL` values.
- Example of API-key: `s1jsa-wm19ASXTXywnzw6ECd0xX`
- Example of URL: `https://gateway-lon.watsonplatform.net/language-translator/api`

:warning: *You are responsible for securing your own credentials. Any user with your service credentials can access your service instances!*

## Your first AI command
Now you can use cURL to invoke language translation using your service credentials, i.e. {apikey} and {url} copied above.

General format of a cURL command is:
```
curl -X POST -u user:password --header "header-string" --data "data-string" URL
```

cURL command for WDC, using apikey, url and JSON format, for English-to-Spanish(en-es) translation, becomes:
```
curl -X POST -u "apikey:{apikey}" --header "Content-Type: application/json" --data "{\"text\": [\"Hello, world! \", \"How are you?\"], \"model_id\":\"en-es\"}" "{url}/v3/translate?version=2018-05-01"
```

:dart: A long command can be split into multiple lines, with the end-of-line continuation character as a backslash `\` in Linux and a caret `^` in Windows.

For the obtained credentials, replace
- {apikey}    by `s1jsa-wm19ASXTXywnzw6ECd0xX`
- {url}       by `https://gateway-lon.watsonplatform.net/language-translator/api`

:dart: Use a plain-text editor to make the complete long command (shown below in multiple lines for Windows)  

```
curl -X POST -u "apikey:s1jsa-wm19ASXTXywnzw6ECd0xX" --header "Content-Type: application/json" ^
--data "{\"text\": [\"Hello, world! \", \"How are you?\"], \"model_id\":\"en-es\"}" ^
"https://gateway-lon.watsonplatform.net/language-translator/api/v3/translate?version=2018-05-01"
```

Issue the complete command at the prompt.

:warning: *Make sure you are online for this command to succeed.*

If everything goes well, you'll get Spanish result from Watson in JSON format!
```
{
  "translations" : [ {
    "translation" : "-í Hola, mundo! "
  }, {
    "translation" : "-+C+¦mo est+ís?"
  } ],
  "word_count" : 5,
  "character_count" : 26
}
```
Result contains the
- Spanish text for each input line
- Number of translated words
- Total number of characters in the result

Another translation, this time from English-to-French (en-fr):
```
curl -X POST -u "apikey:s1jsa-wm19ASXTXywnzw6ECd0xX" --header "Content-Type: application/json" --data "{\"text\": [\"I am learning IBM Watson! \"], \"model_id\":\"en-fr\"}" "https://gateway-lon.watsonplatform.net/language-translator/api/v3/translate?version=2018-05-01"
```

Starting learning French!
```
{
  "translations" : [ {
    "translation" : "J'apprais IBM Watson ! "
  } ],
  "word_count" : 6,
  "character_count" : 26
}
```

Recognize a language with confidence ratings
```
curl -X POST -u "apikey:s1jsa-wm19ASXTXywnzw6ECd0xX" --header "Content-Type: text/plain" --data "Language Translator translates text from one language to another" "https://gateway-lon.watsonplatform.net/language-translator/api/v3/identify?version=2018-05-01"
```

**Congratulation! You just learnt the basics of IBM Watson that will be useful for developing more complex AI applications.**:rocket:

## Python App for Translation
Now we can develop a Python standalone app for language translation.

Following references will help to go ahead!
- [Official documentation on language translation](https://www.ibm.com/watson/services/language-translator/)
- [Reference code for language translation](https://cloud.ibm.com/apidocs/language-translator?code=python#translate)
- [Example code for language translation](https://github.com/watson-developer-cloud/python-sdk/blob/master/examples/language_translator_v3.py)


## Documentation
You can access the documentation by selecting API Reference in the Watson menu (**Watson -> API Reference**).

Here is the complete documentation for the [language translation service](https://cloud.ibm.com/apidocs/language-translator)

## Questions
If you are having difficulties using the APIs or have a question about the IBM Watson Services, please ask a question on
[dW Answers](https://developer.ibm.com/answers/questions/ask/?topics=watson)
or [Stack Overflow](http://stackoverflow.com/questions/ask?tags=ibm-watson).

## Open Source @ IBM
Find more open source projects on the [IBM Github Page](http://ibm.github.io/).

# IBM Watson usage across the world
## Industries
### Health
### Finance

## Fun
### Your kool project here
