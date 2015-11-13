# plcrashreporter

## Building plcrashreporter for buddybuild

- Use Xcode 7.0.1
 > If bitcode is enabled for *any* app component, then Apple mandate that it must be enabled for
 > *all* app components; otherwise Xcode build will fail. Since we do not know if a customer app
 > will have bitcode enabled or not, then we must conservatively assume that bitcode is enabled.

 > In Xcode 7.1 Apple introduced a further restriction where it is no longer possible to compile for
 > MacOS if the `ENABLE_BITCODE=YES`, since the setting is not supported for that platform. This
 > prevents us from building the plcrashreporter framework with `ENABLE_BITCODE=YES`. As a
 > workaround, until a better solution can be found, we avoid using Xcode 7.1 or later.

 ```
xcode-select -p /Applications/Xcode-7.0.1.app
```

Build the iOS archive with the fatass bitcode:

```xcodebuild -configuration Release -scheme CrashReporter-iOS archive OTHER_CFLAGS='-fembed-bitcode'```

The products will land somewhere in your derived data. Copy this into your BBSDK dir and build the SDK.


#OLD INSTRUCTIONS
(These don't generate the fatass bitcode we need)
- build
 ```
xcodebuild -configuration Release -target 'Disk Image'
```

- remove old plcrashreport framework from buddybuild SDK
 ```
rm -rf  $BUDDYBUILD_SDK_ROOT/BuddyBuildSDK/
```

- install the new plcrashreporter framework in the buddybuild SDK
 ```
cp -r 'build/Release/PLCrashReporter-1.2.1/iOS Framework/CrashReporter.framework' $BUDDYBUILD_SDK_ROOT/BuddyBuildSDK/
```
 
