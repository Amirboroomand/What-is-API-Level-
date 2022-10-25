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
  
#Testing against higher API Levels
  
After compiling your application, you should make sure to test it on the platform specified in the application's android:minSdkVersion attribute. To do so, create an AVD that uses the platform version required by your application. Additionally, to ensure forward-compatibility, you should run and test the application on all platforms that use a higher API Level than that used by your application.

The Android SDK includes multiple platform versions that you can use, including the latest version, and provides an updater tool that you can use to download other platform versions as necessary.

To access the updater, use the android command-line tool, located in the <sdk>/tools directory. You can launch the Updater by using the android command without specifying any options. You can also simply double-click the android.bat (Windows) or android (OS X/Linux) file. In ADT, you can also access the updater by selecting Window > Android SDK and AVD Manager.

To run your application against different platform versions in the emulator, create an AVD for each platform version that you want to test. For more information about AVDs, see Android Virtual Devices. If you are using a physical device for testing, ensure that you know the API Level of the Android platform it runs. See the table at the top of this document for a list of platform versions and their API Levels.

#Using a Provisional API Level

In some cases, an "Early Look" Android SDK platform may be available. To let you begin developing on the platform although the APIs may not be final, the platform's API Level integer will not be specified. You must instead use the platform's provisional API Level in your application manifest, in order to build applications against the platform. A provisional API Level is not an integer, but a string matching the codename of the unreleased platform version. The provisional API Level will be specified in the release notes for the Early Look SDK release notes and is case-sensitive.

The use of a provisional API Level is designed to protect developers and device users from inadvertently publishing or installing applications based on the Early Look framework API, which may not run properly on actual devices running the final system image.

The provisional API Level will only be valid while using the Early Look SDK and can only be used to run applications in the emulator. An application using the provisional API Level can never be installed on an Android device. At the final release of the platform, you must replace any instances of the provisional API Level in your application manifest with the final platform's actual API Level integer.
  
  
#Filtering the Reference Documentation by API Level
  
Reference documentation pages on the Android Developers site offer a "Filter by API Level" control in the top-right area of each page. You can use the control to show documentation only for parts of the API that are actually accessible to your application, based on the API Level that it specifies in the android:minSdkVersion attribute of its manifest file.

To use filtering, select the checkbox to enable filtering, just below the page search box. Then set the "Filter by API Level" control to the same API Level as specified by your application. Notice that APIs introduced in a later API Level are then grayed out and their content is masked, since they would not be accessible to your application.

Filtering by API Level in the documentation does not provide a view of what is new or introduced in each API Level — it simply provides a way to view the entire API associated with a given API Level, while excluding API elements introduced in later API Levels.

If you decide that you don't want to filter the API documentation, just disable the feature using the checkbox. By default, API Level filtering is disabled, so that you can view the full framework API, regardless of API Level.

Also note that the reference documentation for individual API elements specifies the API Level at which each element was introduced. The API Level for packages and classes is specified as "Since <api level>" at the top-right corner of the content area on each documentation page. The API Level for class members is specified in their detailed description headers, at the right margin.


