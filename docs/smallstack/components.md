# Smallstack Components
A smallstack component is an isolated part of a website that can be reused across different pages or web projects. They can serve a UI,  fullfill some business logic or both. The smallstack framework already has a lot of components, but sometimes it is necessary to create new ones e.g. for special needs in a different project. Nevertheless, the intention to create a components shall always be as generic as it makes sense so that they can be used in many other projects. Components can be shared via NPM or bower packages and have access to all functionality a smallstack client already has.

## Technology
The smallstack framework provides a useful base for all components, including technology agnostic base classes that can be extended as well as an event system for the communication between components and the client itself. On top of that there are extendable base classes for Angular, Angular 2 and React. It is possible to combine components that are written in any UI technology.

## Usage
Smallstack components can be used in the smallstack page builder to plug pages together, comparable to a CMS on steroids. They can also be used in html pages directly, for exampl, to combine some components to one component.

## Data
TBD

## Configuration
TBD

## Sockets
TBD

## How-to create an Angular 1 component
A minimal Angular 1 component exists of a ng.html and a js|ts file. The AngularComponent factory class should be used to create and register a component. It also provides helper methods for adding meta data, component configuration and component sockets.

1. Create a file called componentName.ng.html and add the html markup
2. Create a controller class named componentName.component.ts and add the business logic
