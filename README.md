# Applanga SDK for Xamarin Localization
***
*Version:* ALPHA 0.0.1

*Website:* <https://www.applanga.com> 

*Changelog:* <https://www.applanga.com/changelog/ios>
***


## Table of Contents

  1. [Installation](#installation)
  2. [Configuration](#configuration)
  3. [Usage](#usage)



## Installation
#### NUGET [[?](https://www.nuget.org/)]

1. Add the ApplangaXamarinSDK Nuget package to your main App project, and to your Android and iOS projects. The package contains platform specific code and so must be added to each project that you would like Applanga to work in.

 
## Configuration
1. To start Xamarin Localization with Applanga download the *Applanga Settings File* for your app from the App Overview in the dashboard by clicking the ***[Prepare Release]*** button and then clicking ***[Get Settings File]***.
 
2. Add the *Applanga Settings File* to the Assets folder in your android project. Make sure to set it's build action to AndroidAsset.
 
3. Add the *Applanga Settings File* to the Root folder of your iOS project. Make sure to set it's build action to Content.

## Usage

### Initialisation:

The applanga ApplangaSDK needs to be initialised before any of its features are used. The best place to do this is in the constructor of your first page. For example here we init the sdk in the MainPage of my app:

```
public MainPage()
{
    Applanga.Init(InitializeComponent);
}
```


### Uploading Strings From Resources:

Using the method 

Applanga.UploadStringsFromResClass(System.Type);

You can upload all the strings from your generated Resource classes.

For example, if your class is named AppResources you could upload the stings like so

Applanga.UploadStringsFromResClass(typeof(AppResources));


### Methods:

string Applanga.GetString(string defaultValue,string key, params);

void Applanga.TakeScreenshotWithTag(string tag);

void Applanga.EnableDraftMode();

void Applanga.DisableDraftMode();

bool Applanga.CaptureScreenshot(string language)
