### Common setup to run in both browser and devices
* **Download and install Node.js (v4.2.6 LTS)**

  Following installation, you should be able to invoke node and npm on your command line. If desired, you may optionally use a tool such as nvm or nave to manage your Node.js installation.

* **Download and install a git client (v2.7.0), if you don't already have one**.

  Following installation, you should be able to invoke git on your command line. Even though you won't be using git manually, the CLI does use it behind-the-scenes to download some assets when creating a new project.

* Clone the repo.

* Create the config-variables.js file in `js` folder (FTmobile/public/www/js) and place the following.
  ```
  var AUTH0_CLIENT_ID="oZxgah56qeCV7NVRYo8UO1mzA4u5nOIw";
  var AUTH0_DOMAIN="infratab-staging.auth0.com";
  var accountsServer = "https://accounts.infratab.xyz/";
  var accountsSignUp="https://accounts.infratab.xyz/users/signup/";
  ```
**NOTE :** Do `npm install` (FTMobile\public\www) to run `grunt watch` after pulling code .

* Change the directory to `www` folder(FTMobile/public/www) and run the `npm install` command, which installs the grunt(Grunt v0.4.5)

* Install Grunt-cli using ```npm install -g grunt-cli@0.1.3``` command

* Precompile the handlebars templates
  * Change the directory to the project's grunt-contrib-handlebars folder(i.e FTMobile/public/www/node_modules/grunt-contrib-handlebars) and run `npm install handlebars@4.0.4`.

   * Change the directory to `handlebars` (i.e FTMobile\public\www\node_modules\grunt-contrib-handlebars\node_modules\handlebars) and run `npm install uglify-js@2.4.0)

   **NOTE :** The above step is needed only because, there is some problem with handlebars@4.0.5 and uglify-js@2.4.25 while build app for windows phone.

 * Run `grunt handlebars` to run grunt handlebars tasks

  **NOTE :** Run `grunt handlebars` each time when you add/remove/change `.hbs` files

* Compile sass to css
  * Download [rubyinstaller](http://rubyinstaller.org/downloads) (v2.2.3) and install.

  **NOTE :** To check if ruby is installed or not using `ruby -v` in command prompt with ruby.
  * Change the directory to www folder (i.e: FTMobile/public/www) and Install `gem install sass@3.4.21` in command prompt with ruby.
  * Run `grunt sass` in command prompt with ruby to compile scss.

  **NOTE :** Run `grunt sass` each time when you add/remove/change `.scss` files.

  **NOTE :** To compile handlebars and scss code just do `grunt watch` in command line it will compile automatically on every save of handlebars and scss files.

### Run the app in browser (Not Recommended)

* create server.js file inside the www folder and place the following lines of code

  ```
  "use strict";
var express = require('express');
var app = express();
app.set('port', 8081);
var server = app.listen(app.get('port'), function() {
  console.log('Express server listening on port ' + server.address().port);
});
app.use(express.static(__dirname + "/"));
exports = module.exports = app;
```
* Comment the `this.bindEvents` and uncomment the `this.onDeviceReady` function calls in index.js file
* Comment these two lines of code in index.js file

  ```
  StatusBar.show();
  StatusBar.backgroundColorByHexString("#0097A7");
  ```

* Commen the following 3 lines of code in index.js file
	```
	if(device.platform === "Android"){
	   fileRef.setAttribute("href", "css/android.css"); //do not comment this line of code
	} else if(device.platform === "windows"){
	  fileRef.setAttribute("href", "css/windows.css");
	}
	```
* Change the directory to www folder in command prompt and run `npm install express`
* Run `node server` or `node server.js`
* Check your ip address
*
  In Windows   
  * ipconfig

  In ubuntu
  * ifconfig

* Run `your.ip.address:8081` in browser. //Note replace the your.ip.address with the actuall ip address.

**NOTE:** This is not recommended, Most of the applicaton will not work when you try to run in browser. You need to hardcode many things to make this work. Please try to run in actual device or emulator instead of browser.

#### Run the app in device/emulator

##### Install Cordova CLI

* Install the cordova module using npm utility of Node.js. The cordova module will automatically be downloaded by the npm utility.

on OS X and Linux:

`$Sudo npm install -g cordova@5.3.3`

on Windows:

`npm install -g cordova@5.3.3`

##### Environment setup

* Setup environments for windows and android
 * Install visual studio 2013 comuunity (For windows).
 * [Install android sdk](https://www.youtube.com/watch?v=U12pqIxwuYE).

 **NOTE:** Install stand-alone android sdk, No need to install android studio.

* Change the directory to public folder (cd FTMobile/public)

* Add platforms:

   For windows `cordova platform add windows`

   For android `cordova platform add android@5.0.0`

   **NOTE:** For adding the platforms, run the above commands in git commnand prompt(git-bash), since this project is using [custom `barcode scanner`](https://github.com/Infratab/phonegap-plugin-barcodescanner), which has few modification for [original plugin](https://github.com/phonegap/phonegap-plugin-barcodescanner) for windows phone, if you run these commands from noraml command prompt, it will not clone the custom repo, becuase of that qr code scanner will not work in project.So use git command prompt.

* build the project:

   For windows phone 8.1 `cordova build windows -- --phone`

   For android `cordova build android`

* Run the app

	* In Device:

	  ###### Install the app using command

	     For windows phone 8.1 `cordoa run windows -- --phone`

	     For android `cordova run android`

	     **NOTE:** To run the app in windows phone, you need to register the windows phone if you have not registered yet. To register the windows phone, connect the windows phone to PC and open the `Windows Phone Registration` (You can find this in Windows Phone SDK 8.1) and click on Register button to register you phone.

	  ###### Install the app by copying file(android)/deploying file(windows phone)

	     * To install the app in windows phone,Open the `Windows phone deployment` inside the `Windows Phone Sdk 8.1`, browse the .appxbundle file and click deploy.
	     * To install the app in android, just copy the .apk file and install.

	* In Emulator:

	     For windows phone 8.1 `cordova emulate windows -- --phone`

	     For android `cordova emulate android`


  **NOTE:** If you are facing [this issue](https://github.com/flackr/circ/issues/342), please follow the below steps to over come the issue:
  
  1. Open the SDK manager (from command line, type "android").
  2. Under "Extras", Make sure you have "Android Support Repository" and "Google Repository" downloaded.

## Get necessary certificates and keys(One time for the app)

### For Android

#### 1. Generate .keystore file using following command:

`keytool -genkey -v -keystore <my-release-key.keystore> -alias <alias_name> -keyalg RSA -keysize 2048 -validity 10000`

**NOTE** : `my-release-key.keystore` = keystore file name, `alias_name` = name of alias, these values we are going to use in configuration file(i.e build.json)

For more information refer: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html

This command will generate the .keystorye file, place this file in root directory.

#### 2. Give the configuration details in buid.json file

This needs the details that you have given while generating the .keystore file(above step),

Refer documentation for more details: `signing app section` of this documentation(https://cordova.apache.org/docs/en/dev/guide/platforms/android/tools.html)

### For Windows phone

To sign the app for windows phone, first we need to create the certificate files and we need to give the configuration details in build.json

You can find complete details in this [Documentation!](https://cordova.apache.org/docs/en/5.4.0/guide/platforms/win8/packaging.html)

#### 1. Create Certificate files

For creating certificates we need to use makecert.exe util. This tool ships with Windows SDK and can be found under %ProgramFiles(x86)%\Windows Kits\8.1\bin\x64 or %ProgramFiles(x86)%\Windows Kits\8.1\bin\x86

The first thing we need to do is to create a root key for signing our app.

```
Ex:
makecert.exe -n "CN=FakeCorp.com" -r -eku "1.3.6.1.5.5.7.3.3,1.3.6.1.4.1.311.10.3.13" -e "01/01/2020" –h 0 -sv FakeCorp.com.pvk FakeCorp.com.cer
```

Refer the [Documentation!](https://cordova.apache.org/docs/en/5.4.0/guide/platforms/win8/packaging.html) for complete explaination about the above command.

After running makecert for the first time, enter the private password on the screen that pops up.

Once pvk and cer file is created, we need to create a pfx file from these certificates. A pfx (Personal Exchange Format) file contains a variety of cryptographic information, such as certificates, root authority certificates, certificate chains and private keys. To package the certs, we will use the a tool called pvk2pfx. This tool ships with Windows SDK and can be found under %ProgramFiles(x86)%\Windows Kits\8.1\bin\x64 or %ProgramFiles(x86)%\Windows Kits\8.1\bin\x86.

```
EX:
pvk2pfx -pvk FakeCorp.com.pvk -pi pvkPassword -spc FakeCorp.com.cer -pfx FakeCorp.com.pfx -po pfxPassword
```
Where:

pvk : Input pvk file name,

pi : pvk password

spc : Input cert file name

pfx : Output pfx file name

po : pfx password; same as pvk password if not provided

If we provide this pfx file to build.json file, we will have the following error: "The key file may be password protected. To correct this, try to import the certificate manually into the current user's personal certificate store.". In order to import it we have to use certutil from an admin prompt:

```certutil -user -p PASSWORD -importPFX FakeCorp.com.pfx```

Where:

user : Specifies "current user" personal store

p : Password for pfx file

importPfx : Name of pfx file

Once installed, next step is to add packageThumbprint and packageCertificateKeyFile to build.json. In order to find the packageThumbprint, search for the CommonName we've associated with the certificate:

```powershell -Command " & {dir -path cert:\LocalMachine\My | where { $_.Subject -like \"*FakeCorp.com*\" }}"```



## Get Release apk and appxBundle (Each time while getting the release builds)

* Get the necessary keys and certificates from [this](https://github.com/Infratab/config/tree/master/FTMobile) repo, if you have not done before
* Create build.json file in www folder (FTMobile/public), if you have not created yet.
* Place the following in the build.json file

  ```
  {
	"windows":{
		"release":{
			"publisherId":"", //place the publisher Id
			"packageCertificateKeyFile":"", path to windows_release.pfx file
			"packageThumbprint":"‎" //thumbPrint
		}
	},
	"android": {
         "release": {
             "keystore": "/path/to/android.kystore file",
             "storePassword": "",
             "alias": "",//alias name
             "password" : "",//password
             "keystoreType": ""
         }
     }
}
```

* Change the configuration details by changing the values in config-variales.js(FTMobile/public/www/js/config-variables.js) to production details

* Change the directory in command terminal to the directory where you placed the `build.json`( i.e FTMobile/public as build.json is placed in public folder as specified above section) and run the following commands

* Generate release apk file by running
  `cordova build android --release --buildConfig=build.json`


	**NOTE:** While building the anroid release apk, you might get an error `Build Failed`. If your Build fails then place 	the following code in `android` section in the file `build.gradle` (public/platforms/androidbuild.gradle)

	`
	lintOptions {
	       checkReleaseBuilds false
	   }
	`

* Generate release appxbundle file by running
  `cordova build windows -- --phone --release --buildConfig=build.json`

   **NOTE:** Please check, does the above command has generated `CordovaApp.Phone_<version number>_language-ms.appx`(appx bundle in malaya language). If this is generated, the open the `package.phone.appxbundle` file(FTMobile/platforms/windows/package.phone.appxbundle), remove the `<Resource Language="x-generate" />` line of code and add the following line of codes in that place:

   ```
   <Resource Language="EN-US" />
    <Resource Language="IS-ABSOLUTE" />
    <Resource Language="IS-RELATIVE" />
   ```
