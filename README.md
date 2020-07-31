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

The SDK should be initialised seperatly in your Android and iOS projects.

Once the SDK is ready it will trigger a callback that you can use to populate your views or hide a loading screen etc...

For android, you should call it from your MainActivity.cs file.

Here is an example of how you could adapt the default android App launch to work with applanga init:

```
var myApp = new App();

LoadApplication(myApp);

ApplangaXamarinAndroid.Init(this,(result) =>
{
    ((MainPage)myApp.MainPage).ApplangaInitComplete();
});
```
Note: ANdroid init requires the activity to be passed.

For iOS you should call init from your AppDelegate.cs file, like so

```
var myApp = new App();

LoadApplication(myApp);

ApplangaXamarinIos.Init((result) => {
	((MainPage)myApp.MainPage).ApplangaInitComplete();
});
```
In both examples i am calling a method that i created in my MainPage which updates the texts of all my labels.

### Uploading Strings From Resources:

Using the method 

Applanga.UploadStringsFromResClass(System.Type);

You can upload all the strings from your generated Resource classes.

For example, if your class is named AppResources you could upload the stings like so

Applanga.UploadStringsFromResClass(typeof(AppResources));


### Methods:

Applanga.GetString(defaultValue, key, params);

Applanga.TakeScreenshotWithTag(tag);

Applanga.EnableDraftMode();

Applanga.DisableDraftMode();
