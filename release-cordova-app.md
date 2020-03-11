# 📦 Release Cordova App
* Move curent directory to a cordova project

## Publish your app for first time
* Generate apk in release mode
* Generate Key store file
* Signing your app
* Zip align your apk

## How to update your App
* Increase version number
* Generate release build
* Sign your apk with old keystore
* zipalign your apk

### Let's start
Before generating your release apk, navigate to your **config.xml** file & make the requried changes, such as 
* app name 
* developer details
* app versions e.tc 
Also make sure you've removed all unwanted plugins.

## Step 1: Generate APK in release mode
We need to generate release apk by using

🔨For Cordova Build
```bash
$ ./node_modules/.bin/cordova build --release android
```
🔨For Ionic Build
```
$ ionic cordova build --prod --release android
```
The unsigned APK have been generated to:
`./platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk`

You can see your path on your terminal/cli
!! important !! Rename your apk with yourappname.apk & move the file into the home folder

## 🔑 Step 2: Generate Keystore file
when you generate the keystore file, it'll ask these questions below, please answer those and you have to create a new password for a keystore file too.
```bash
$ keytool -genkey -v -keystore yourappname.keystore -alias yourappname -keyalg RSA -keysize 2048 -validity 10000

keystore password? : xxxxxxx
What is your first and last name? :  xxxxxx
What is the name of your organizational unit? :  xxxxxxxx
What is the name of your organization? :  xxxxxxxxx
What is the name of your City or Locality? :  xxxxxxx
What is the name of your State or Province? :  xxxxx
What is the two-letter country code for this unit? :  xxx
```
**NOTE:** After the command above and after filling out the informations, the keystore will be generated to:
`./[KEYSTORE_NAME].keystore`.
You have to move it next to the unsigned APK file.

## ✒️ Sign
* *Move to the unsigned APK directory*
    ```bash
    $ cd ./platforms/android/app/build/outputs/apk/release
    ```
## Step 3: Signing your application using jarsigner
Before executing this step, you must keep your release apk & keystore file in the same folder.
```xml
$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore yourappname.keystore yourappname.apk yourappname
```

## Step 4: Zip align your apk
````
$ zipalign -v 4 yourappname.apk yourappname-final.apk
```
**Note** If you're facing any issue like zipalign is not an internal or external command, you need to set a path for android build tools.please read this setup documentation
[ionic-cordova](https://codesundar.com/ionic-cordova-environment-setup-for-windows-mac/)

**IMPORTANT** : please backup your keystore file, password & alias_name.because it's very important for next update. Incase, if you forget your password, you can't recover it :(

# How to update your Ionic apps on PlayStore?

If you have released the app & want to update the app from playstore for next version? follow these guidelines

## Step 1: Update the version name
Navigate to your config.xml & increase your version number

## Step 2: Generate APK in release mode
We need to generate release apk by using

For Cordova
```bash
$ ./node_modules/.bin/cordova build --release android
```
For Ionic
```
$ ./node_modules/.bin/ionic cordova build --prod --release android
```
This will generate release apk in platforms/android/build/outputs/apk/android-relase-unsigned.apk You can see your path on your terminal/cli
!! important !! Rename your apk with yourappname.apk & move the file into the home folder

## Step 3: Signing your application using jarsigner
Before executing this step, you must keep your release apk & keystore file in the same folder.
```
$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore yourappname.keystore yourappname.apk yourappname
```

## Step 4: Zip align your apk

```
$ zipalign -v 4 yourappname.apk yourappname-final.apk
```
## ❤️ In Conclusion

Create a Google Play account and upload the APK file to playstore

