# How-to setup & install smallstack

## Initial Setup

### OS Support
Currently, smallstack projects run on Windows, Linux and MacOS. 

### Prerequisites
In order to compile, use or deploy a smallstack project you need to install the following dependencies:

#### Node & NPM
We recommend to install the current LTS version of node and the related npm version. Instructions can be found here: https://nodejs.org

#### Meteor 
See https://guide.meteor.com/#quickstart

#### CLI Tool
Please install our opensource command line tool. You probably need to install it with administration rights:
```
npm install -g smallstack-cli
```


## Setup
There are 4 ways to get the smallstack framework sources into your project, some of them require a "Developer License" which you can get on our website (smallstack.io). If you navigate to the project root folder and hit 'smallstack setup' you will be asked which way you prefer:

### Project Version
This is the easiest way. The CLI tool will read the smallstack version from your project, connect to smallstack.io and download the necessary files. You can change the smallstack project version inside the root package.json!

### Local Checkout
If you are developing or extending the smallstack framework itself it makes sense to work directly on a local checkout. This requires a smallstack developer license.

### Local File
In very rare cases you might got a smallstack.zip from us. In this case, you just have to provide the path.

### Remote File
If you got a link from us to a smallstack release, please use this option!
