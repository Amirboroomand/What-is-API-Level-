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


