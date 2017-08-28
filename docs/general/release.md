# Building a new Release
Before you can deploy your newest bundle to the cloud, you have to make a new release. 

## Make Release
In any git tool of your choice, for example Sourcetree, you should:
* merge all finished feature branches to your develop branch
* check version you want to deploy (smallstack gitflow --toVersion=0.7.0)
* then start a new release with Git Flow -> Start new Release. You have to give a version number or tag. 
* on a project release, you have to edit the package.json with the new smallstack version.
* do the same with finish current release. 
* on the master branch, you should push all merge commits. 

## Publish the release in docker cloud
* now our CI tool jenkins will building a new bundle for that release. Got to https://jenkins.smallstack.io to see, if the build succeeded.
* if everythings works fine, jenkins will upload the bundle named as version-branch-builddate.tar.gz to the specified S3 bucket on AWS.
* all you have to do, is make the file public and copy the bundle name
* now login to docker, navigate to the service you want to update and adjust the bundle url. Hit Redeploy
* switch to develop and set new version with smallstack gitflow --toVersion=0.8.0

## Make mobile App Update
* to update your Android app, simply create your APK file with the command:
`tns build android --release --key-store-path ./path/to/keystore.file --key-store-password 'yourKeystorePassword' --key-store-alias your-keystore-alias --key-store-alias-password 'yourKeystoreAliasPassword' --copyTo ./path/to/copy/the/apk-file`

* to update your ios app, start XCode and open the project workspace.
* in the signing options select the right team 
* clean, build the project and then archive. 
* if you run into following error:
`Showing Recent Issues`
`diff: /Podfile.lock: No such file or directory`
`diff: /Manifest.lock: No such file or directory`
`error: The sandbox is not in sync with the Podfile.lock. Run 'pod install' or update your CocoaPods installation.`
* Close XCode
* run `tns publish ios` 
* open XCode again and re-run clean, build, archive
* sometimes it helps to re-install your pod-files with `pod install`
