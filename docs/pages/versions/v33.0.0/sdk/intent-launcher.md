---
title: IntentLauncher
---

Provides a way to launch android intents. e.g. - opening a specific settings screen.

## Installation

This API is pre-installed in [managed](../../introduction/managed-vs-bare/#managed-workflow) apps. To use it in a [bare](../../introduction/managed-vs-bare/#bare-workflow) React Native app, follow its [installation instructions](https://github.com/expo/expo/tree/master/packages/expo-intent-launcher).

## API

```js
import * as IntentLauncher from 'expo-intent-launcher';
```

### `IntentLauncher.startActivityAsync(activityAction, intentParams)`

Starts the specified activity. The method will return a promise which resolves when the user returns to the app.

#### Arguments

- **activityAction (_string_)** -- The action to be performed, e.g. `IntentLauncher.ACTION_WIRELESS_SETTINGS`. There are a few pre-defined constants you can use for this parameter. You can find them at [expo-intent-launcher/src/IntentLauncher.ts](https://github.com/expo/expo/blob/master/packages/expo-intent-launcher/src/IntentLauncher.ts). **Required**
- **intentParams ([`IntentParams`](#typeintentparams))** -- An object of intent parameters.

#### Returns

A promise resolving to an object of type [IntentResult](#typeintentresult).

## Types

### Type `IntentParams`

| Key         |  Type  | Description                                                                                                                                                                                                                       |
| ----------- | :----: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type        | string | A string specifying the MIME type of the data represented by the `data` parameter. Ignore this argument to allow Android to infer the correct MIME type.                                                                          |
| category    | string | Category provides more details about the action the intent performs. See [Intent.addCategory](<https://developer.android.com/reference/android/content/Intent.html#addCategory(java.lang.String)>).                               |
| extra       | object | A map specifying additional key-value pairs which are passed with the intent as `extras`. The keys must include a package prefix, for example the app `com.android.contacts` would use names like `com.android.contacts.ShowAll`. |
| data        | string | A URI specifying the data that the intent should operate upon. (_Note: Android requires the URI scheme to be lowercase, unlike the formal RFC._)                                                                                  |
| flags       | number | Bitmask of flags to be used. See [Intent.setFlags](<https://developer.android.com/reference/android/content/Intent.html#setFlags(int)>) for more details.                                                                         |
| packageName | string | Package name used as an identifier of ComponentName. Set this only if you want to explicitly set the component to handle the intent.                                                                                              |
| className   | string | Class name of the ComponentName.                                                                                                                                                                                                  |

### Type `IntentResult`

| Key        |  Type  | Description                                                                               |
| ---------- | :----: | ----------------------------------------------------------------------------------------- |
| resultCode | number | Result code returned by the activity. See [ResultCode](#enumresultcode) for more details. |
| data       | string | Optional data URI that can be returned by the activity.                                   |
| extra      | object | Optional extras object that can be returned by the activity.                              |

## Enums

### Enum `ResultCode`

| Result code | Value | Description                                                               |
| ----------- | :---: | ------------------------------------------------------------------------- |
| Success     |  -1   | Indicates that the activity operation succeeded.                          |
| Canceled    |   0   | Means that the activity was canceled, e.g. by tapping on the back button. |
| FirstUser   |   1   | First custom, user-defined value that can be returned by the activity.    |

#### Example

```javascript
import * as IntentLauncher from 'expo-intent-launcher';

// Open location settings
IntentLauncher.startActivityAsync(IntentLauncherAndroid.ACTION_LOCATION_SOURCE_SETTINGS);
```