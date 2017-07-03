# Bundling & Deploying
When it comes to deploying and bundling we differ between smallstack projects, the smallstack framework itself and smallstack components.

# Bundling

## Bundling a project
The underlaying frameworks for projects are Meteor for Web & Server and Nativescript for Mobile Apps. 

### Bundling Meteor
Either you do it the meteor way (https://docs.meteor.com) or you use our CLI tool:
* Goto the root folder of your smallstack project
* Call `smallstack clean generate bundle`to create a clean bundle

You'll find the "meteor.tar.gz" file in /built.

### Bundling the Nativescript App
Please refer to the official documentation since this process changes quite often: https://docs.nativescript.org. Right now we're doing just fine with changing to the nativescript folder and calling `tns build android`, which creates an unsigned APK, and `tns build ios` which produces an XCode Project. 

## Bundling the framework
The bundling process is currently done by NPM and rollup as bundler itself. 

* Goto the root folder of the smallstack framework
* Call `smallstack clean generate bundle` to create a clean bundle

After some minutes you can find the generated smallstack*.zip in the subdirectory /dist. If you want to reference this file in an automated process you can reference the symlink /dist/smallstack.zip!
