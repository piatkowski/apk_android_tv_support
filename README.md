# Step 1. Decompile APK with apktool

```
apktool d Input.apk
```

# Step 2. Modify manifest

1. Open AndroidManifest.xml

2. Add features

```xml
<uses-feature android:name="android.software.leanback" android:required="true" />
<uses-feature android:name="android.hardware.faketouch" android:required="false" />
<uses-feature android:name="android.hardware.touchscreen" android:required="false" />
```

3. Remove any permission related to mobile phone or tablet for example: camera, touchscreen, sensors, etc.

4. Add banner

```xml
<application ... android:banner="@drawable/...">
```

5. Change orientation, look for android:screenOrientation

```
android:screenOrientation="landscape"
```

6. Add leanback in intent-filter in main acitivty

```xml
<category android:name="android.intent.category.LEANBACK_LAUNCHER" />
```

7. Save xml file

# Step 3. Rebuild APK

```
apktool b decompiled-apk-folder/ Output.apk
```

# Step 4. Sign APK

```
java -jar signapk.jar certificate.pem key.pk8 decompiled-apk-folder/dist/Output.apk ./Ouput_signed.apk
```

# Step 5. Align APK

```
zipalign -p -f -v 4 Output_signed.apk Output_signed_aligned.apk
```

# Step 6. Install

Upload APK to device and install Output_signed_aligned.apk

# Notes

In some cases you can try change order of sign and align commands.
