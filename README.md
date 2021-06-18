# Ionic over ApiRTC/angular Steps by Steps Tutorial

Tutorial for building a WebRTC **mobile app** from **web app** available at https://github.com/ApiRTC/ApiRTC-angular.

## Install Ionic :

`sudo npm install -g @ionic/cli`

Note : This tutorial was made with **Ionic cli 6.16.1**.

## Clone ApiRTC-angular app

Clone with renaming with ionic suffix if you already have cloned ApiRTC-angular :

`git clone https://github.com/ApiRTC/ApiRTC-angular.git ApiRTC-angular-ionic`

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

### For Android

Add Android capacitor :

`ionic cap add android`

If working on linux, configure `CAPACITOR_ANDROID_STUDIO_PATH` env variable (with your own /path/to) :

    export CAPACITOR_ANDROID_STUDIO_PATH=/path/to/android-studio/bin/studio.sh
    
Handle Android permissions :

`npm install @ionic-native/android-permissions`

In `app.module.ts` :

    import { AndroidPermissions } from '@ionic-native/android-permissions/ngx';
    ...
    providers: [AndroidPermissions],
    ...

In `app.component.ts` :

    constructor(private fb: FormBuilder,
        private androidPermissions: AndroidPermissions) {

        this.androidPermissions.checkPermission(this.androidPermissions.PERMISSION.CAMERA).then(
          result => console.log('Has permission?', result.hasPermission),
          err => this.androidPermissions.requestPermission(this.androidPermissions.PERMISSION.CAMERA)
        );

        this.androidPermissions.requestPermissions([this.androidPermissions.PERMISSION.CAMERA, this.androidPermissions.PERMISSION.GET_ACCOUNTS]);
    }

Open in studio :

`ionic cap open android`

In AndroidManifest.xml :

    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />

From **AndroidStudio**, you can run the app on your device or an AVD. You can use the original angular app as a peer, or even the live **pureJS** demo at https://apizee.github.io/ApiRTC-examples/conferencing/index.html

### For iOS

Please note that **IOS 14.5+** is required.

Edit `src/index.html` to add content top-offset for iOS :

`<ion-content style="position:absolute; top:40px" overflow-scroll="true">`

Add iOS capacitor :

`ionic cap add ios`

`ionic cap open ios`

Setup certificates inside *Xcode -> Signing & Capabilities* project section.

Then build from Xcode.

## Modify 

To take into account code modification, run :

`ionic build --project="ApiRTC-angular"`

`ionic cap copy --project="ApiRTC-angular"`
