- .gradle
	- configurations and files used for project building
		- automatically generated when you try to compile a project
- .idea
	- project metadata
		- tell the app how to use data
	- configuration files
		- compiler.xml
		- encodings.xml
		- modules.xml
- app
	- project source code
- gradle
	- build-related data
		- .gitignore
		- build.gradle
		- gradlew
			- create once, then keep updating
		- local.properties
			- local configuration information
		- settings.gradle
			- handle settings

---
# Activity Class
	MainActivity.kt

Activity is an entry point for interacting with the user.

- layout
	- UI

In the design, we have a main activity template which is `MainActivity.kt`

One important function is `onCreate()` which is the entry point of the activity.

---

# Gradle

A set of build configuration files
- how a project is to be ==developed==
- what ==dependencies== need to exist for the project to build and run successfully
- what the ==result== or results of the compilation process should be

There are two `build.gradle` files
- one setting applies to every module in the entire project
- one setting applies to only the app module

``` build.gradle
apply plugin: 'com.android.;application'

android {
	defaultConfig{...}
	buildTypes{...}
}

dependencies{...}
```

`./gradlew build`
- build a project when you are ready to run the application

`./gradlew clean`
- delete the contents of the build directory already generated

`./gradlew wrapper`
- see all available gradle operations running in the background

---

# Manifest

When a project is created, a `manifest.xml` is generated. It contains info about the app which helps you define permissions.
- camera access
- GPS
- gallery

## Tags
- `<uses-permission android:name="android.permission.SEND_SMS"> </uses-permission>`
	- allow the app to send SMS
- `<application android:theme="@style/Theme.SampleApp">`
	- set the theme from a local file
	- `<activity android:theme="@style/Theme.SampleApp.NoActionbar">`
		- a sub-tag defining activities
		- `<intent-filter>`
			- a sub-sub-tag defining which is the first activity
				- `<action android:name="android.intent.action.MAIN"/>`
				- `<category android:name="android.intent.category.LAUNCHER"/>`

---

# Resource Folder

	Can be referenced anywhere

- string
	- `res/values/strings.xml`
		- `<resource> <string name="message"> Congras! </string> </resource>`
- color
	- `color.xml`
- dimension
	- `dimens.xml`
		- `<resource> <dimen name="fab_margin"> 16dp </dimen> </resource>`
- font

Providing default resource helps compatibility.

---

# drawable and mipmap

	mipmap is an upgrade of drawable. They are both used to store image assets.

mipmap ensures that your app renders high-quality images across different devices.
- same image but different resolution in different folders

---

# layout

- used to manage the UI
- contains 4 `.xml` files
- `.xml` files separate the presentation from the code

