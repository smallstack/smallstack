# Building a new Release
Before you can deploy your newest bundle to the cloud, you have to make a new release. 

## Make Release
In any git tool of your choice, for example Sourcetree, you should:
* merge all finished feature branches to your develop branch
* then start a new release with Git Flow -> Start new Release. You have to give a version number or tag. 
* do the same with finish current release. 
* on the master branch, you should push all merge commits. 

## Publish the release in docker cloud
* now our CI tool jenkins will building a new bundle for that release. Got to https://jenkins.smallstack.io to see, if the build succeeded.
* if everythings works fine, jenkins will upload the bundle named as version-branch-builddate.tar.gz to the specified S3 bucket on AWS.
* all you have to do, is make the file public and copy the bundle name
* now login to docker, navigate to the service you want to update and adjust the bundle url. Hit Redeploy
