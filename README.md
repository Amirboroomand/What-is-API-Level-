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


