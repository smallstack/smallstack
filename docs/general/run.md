# How-to run a smallstack project
If you have installed all dependencies and did the smallstack setup dance, you can now start the project. The first time it feels like downloading half of the internet due a lot of npm dependencies, but the second time it will be blazing fast already. This is normally done by 

## A note about the local smallstack checkout mode
If you have a local checkout of smallstack, you first need to initially bundle the framework:
- Navigate to the root of your smallstack checkout
- Call 'smallstack setup' to initialize your local copy
- Call 'smallstack generate' to execute the source code generation based on the smallstack typesystem
- Call 'smallstack bundle' to bundle all smallstack modules into a single zip file

Afterwards, you can use 'smallstack setup' with the local checkout or local file mode inside your project directory.

# starting the server
- Navigate to the root of your project and then to the meteor folder
- Call 'meteor' to start the meteor server
- After meteor is up, you can visit http://localhost:3000 to view your project
