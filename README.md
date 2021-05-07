# ApiRTC-angular-ionic-tutorial

Tutorial for building an **ApiRTC** **webapp** developped in **angular** with **ionic**.

## Install Ionic :

`sudo npm install -g @ionic/cli`

## Clone ApiRTC-angular app

Clone with renaming with ionic suffix if you already have cloned ApiRTC-angular :

`git clone https://github.com/apizee/ApiRTC-angular.git ApiRTC-angular-ionic`

## Add @ionic/angular to the app

`cd ApiRTC-angular-ionic`

`ng add @ionic/angular`

## Ionic-ize the app 

`ionic init`

 => give same name as the angular app : `ApiRTC-angular`

Edit `angular.json` to modify `outputPath` with :

	"outputPath": "www",
	
Edit `src/index.html` to modify `<base href` and wrap `<app-root>` into `<ion-content>` to enable scroll :

    <base href="./">
    <body>
        <ion-content overflow-scroll="true">
            <app-root></app-root>
        </ion-content>
    </body>


## Build

`ionic build --project="ApiRTC-angular"`

## For Android

Add Android capacitor :

`ionic cap add android`

If working on linux and want to work with Android : add linuxAndroidStudioPath in capacitor.config.json :

    {
      "appId": "io.ionic.starter",
      "appName": "ApiRTC-angular",
      "bundledWebRuntime": false,
      "npmClient": "npm",
      "webDir": "www",
      "plugins": {
        "SplashScreen": {
          "launchShowDuration": 0
        }
      },
      "cordova": {},
      "linuxAndroidStudioPath": "/home/kmoyse/opt/android-studio/bin/studio.sh"    
    }

Open in studio :

`ionic cap open android`

From Studio, you can run the App on your device or an AVD. You can use the original angular app as a peer, or even the live pure JS demo at https://apizee.github.io/ApiRTC-examples/conferencing/index.html

## For IOS

// TODO

## Modify 

To take into account code modification, run :

`ionic build --project="ApiRTC-angular"`

`ionic cap copy --project="ApiRTC-angular"`
