# What-is-API-Level
API Level is an integer value that uniquely identifies the framework API revision offered by a version of the Android platform.

The Android platform provides a framework API that applications 
can use to interact with the underlying Android system. 
The framework API consists of:

•A core set of packages and classes
•A set of XML elements and attributes for declaring a manifest file
•A set of XML elements and attributes for declaring and accessing resources
•A set of Intents
•A set of permissions that applications can request, as well as permission enforcements included in the system


The API Level identifier serves a key role in ensuring the best possible experience for users and application developers:

•It lets the Android platform describe the maximum framework API revision that it supports
•It lets applications describe the framework API revision that they require
•It lets the system negotiate the installation of applications on the user's device, such that version-incompatible •applications are not installed.


Each Android platform version stores its API Level identifier internally, in the Android system itself.

Applications can use a manifest element provided by the framework API — <uses-sdk> — to describe the minimum and maximum API Levels under which they are able to run, as well as the preferred API Level that they are designed to support. The element offers three key attributes:

android:minSdkVersion — Specifies the minimum API Level on which the application is able to run. The default value is "1".
android:targetSdkVersion — Specifies the API Level on which the application is designed to run. In some cases, this allows the application to use manifest elements or behaviors defined in the target API Level, rather than being restricted to using only those defined for the minimum API Level.
android:maxSdkVersion — Specifies the maximum API Level on which the application is able to run. Important: Please read the <uses-sdk> documentation before using this attribute.


For example, to specify the minimum system API Level that an application requires in order to run, the application would include in its manifest a <uses-sdk> element with a android:minSdkVersion attribute. The value of android:minSdkVersion would be the integer corresponding to the API Level of the earliest version of the Android platform under which the application can run.

When the user attempts to install an application, or when revalidating an appplication after a system update, the Android system first checks the <uses-sdk> attributes in the application's manifest and compares the values against its own internal API Level. The system allows the installation to begin only if these conditions are met:

If a android:minSdkVersion attribute is declared, its value must be less than or equal to the system's API Level integer. If not declared, the system assumes that the application requires API Level 1.
If a android:maxSdkVersion attribute is declared, its value must be equal to or greater than the system's API Level integer. If not declared, the system assumes that the application has no maximum API Level. Please read the <uses-sdk> documentation for more information about how the system handles this attribute.


When declared in an application's manifest, a <uses-sdk> element might look like this:

<manifest>
  <uses-sdk android:minSdkVersion="5" />
  ...
</manifest>


#Development Considerations

The sections below provide information related to API level that you should consider when developing your application.

#Application forward compatibility

Android applications are generally forward-compatible with new versions of the Android platform.

Because almost all changes to the framework API are additive, an Android application developed using any given version of the API (as specified by its API Level) is forward-compatible with later versions of the Android platform and higher API levels. The application should be able to run on all later versions of the Android platform, except in isolated cases where the application uses a part of the API that is later removed for some reason.

Forward compatibility is important because many Android-powered devices receive over-the-air (OTA) system updates. The user may install your application and use it successfully, then later receive an OTA update to a new version of the Android platform. Once the update is installed, your application will run in a new run-time version of the environment, but one that has the API and system capabilities that your application depends on.

In some cases, changes below the API, such those in the underlying system itself, may affect your application when it is run in the new environment. For that reason it's important for you, as the application developer, to understand how the application will look and behave in each system environment. To help you test your application on various versions of the Android platform, the Android SDK includes multiple platforms that you can download. Each platform includes a compatible system image that you can run in an AVD, to test your application.

#Application backward compatibility

Android applications are not necessarily backward compatible with versions of the Android platform older than the version against which they were compiled.

Each new version of the Android platform can include new framework APIs, such as those that give applications access to new platform capabilities or replace existing API parts. The new APIs are accessible to applications when running on the new platform and, as mentioned above, also when running on later versions of the platform, as specified by API Level. Conversely, because earlier versions of the platform do not include the new APIs, applications that use the new APIs are unable to run on those platforms.

Although it's unlikely that an Android-powered device would be downgraded to a previous version of the platform, it's important to realize that there are likely to be many devices in the field that run earlier versions of the platform. Even among devices that receive OTA updates, some might lag and might not receive an update for a significant amount of time.

#Selecting a platform version and API Level

When you are developing your application, you will need to choose the platform version against which you will compile the application. In general, you should compile your application against the lowest possible version of the platform that your application can support.

You can determine the lowest possible platform version by compiling the application against successively lower build targets. After you determine the lowest version, you should create an AVD using the corresponding platform version (and API Level) and fully test your application. Make sure to declare a android:minSdkVersion attribute in the application's manifest and set its value to the API Level of the platform version.

#Declaring a minimum API Level

If you build an application that uses APIs or system features introduced in the latest platform version, you should set the android:minSdkVersion attribute to the API Level of the latest platform version. This ensures that users will only be able to install your application if their devices are running a compatible version of the Android platform. In turn, this ensures that your application can function properly on their devices.

If your application uses APIs introduced in the latest platform version but does not declare a android:minSdkVersion attribute, then it will run properly on devices running the latest version of the platform, but not on devices running earlier versions of the platform. In the latter case, the application will crash at runtime when it tries to use APIs that don't exist on the earlier versions.


