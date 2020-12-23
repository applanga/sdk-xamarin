# Applanga SDK for Xamarin Localization
***
*Version:* ALPHA 0.0.2

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

### Initialisation and basic usage:

The applanga ApplangaSDK needs to be initialised before any of its features are used. The best place to do this is in the constructor of your first page.

When using applanga you can choose between 2 different init methods and usage patterns.

#### 1: Automatic Translation and string upload

In order to use the auto translation and string upload features in applanga, you need to init the sdk with the 'Type' of your auto generated Resources class/ Most commenly this is named AppResources, but can also be named differently.

By doing this, applanga will automatically upload the strings to the Applanga dashboard and it will automatically translate any texts you access from your resources class.

Here is an example of this init method:

```
public MainPage()
{
   Applanga.Init(typeof(AppResources),InitializeComponent);
}
```
If you use this init method, then you will not have to make any changes to your code or xml layouts, applanga will automatically present the latests translations for the current language.

#### 2: Manual Translation

If you do not want to use the automatic features of the SDK, then you can still access most features manually. Init the SDK without the Resource Class type, like so:

```
public MainPage()
{
    Applanga.Init(InitializeComponent);
}
```
Then to access translations in code you can do like this:

```
ExampleLabel.text = Applanga.GetString("text_key","default_value");
```
And in your xml layouts you can access translations using the Applanga MarkupExtention.

First import it to your layout file header like so:

```
<ContentPage ... 
             xmlns:local="clr-namespace:ApplangaSDK.Xamarin;assembly=ApplangaXamarinSdk.Base">
             
```
then in the layout you can access translations like so:

```
<Button Text="{local:Applanga text_key}"
                VerticalOptions="CenterAndExpand"
                HorizontalOptions="Center"
                x:Name="DisableDraftModeButton"/>

```

### Update content
To get the latest translations for the current language, you can call the update method any time after init like so:

```
void Applanga.Update(Action<bool> callback);

```
NOTE: this happens automatically on init of the SDK, so you only need to use this method if you change the language at runtime manually

### Manual language change:

You can change your app language at runtime using the following call:

```
bool SetLanguage(string language);
```
  *language* must be the iso string of a language that has been added in     the dashboard.
      The return value will be *true* if the language could be set, or if it already was the     current language, otherwise it will be *false*. After a successful call you should      recreate the current activity, for the changes to take effect.
      The set language will be saved, to reset to the     device language call:

```
ApplangaSetLanguage(null);
```

For the app to reset to the device language it needs to be restarted.

The *language* parameter is expected in the format **[language]-[region]** or     **[language]_[region]** with region being optional. Examples: "fr_CA", "en-us", "de".

If you wish to make sure that the language that has been changed to has the latest texts, then you need to call Applanga.Update directly after the SetLanguage call.

### Draft Mode:

To enable or disable [Draft Mode](https://www.applanga.com/docs/translation-management-dashboard/draft_on-device-testing) you can use the following methods: 

```
void Applanga.EnableDraftMode();

void Applanga.DisableDraftMode();

```

### Screenshots:


The Applanga SDK offers the functionality to upload screenshots of your app, while collecting meta data such as the current language, resolution and the Applanga translated strings that are visible,     including their positions.
     Each screenshot will be assigned to a tag. A tag may have multiple screenshots with differing core meta data: language, app version, device, plattform, OS and resolution.

You can read more here: [Manage Tags](https://applanga.com/docs#manage_tags) and here: [Uploading screenshots](https://applanga.com/docs#uploading_screenshots).

To capture screenshots for the Applanga dashboard you can use the following method

```
void CaptureScreenshot(string tag);
```
