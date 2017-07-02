# Smallstack Components
A smallstack component is an isolated part of a website that can be reused across different pages or web projects. It can serve a UI,  fullfill some business logic or both. The smallstack framework already has a lot of components, but sometimes it is necessary to create new ones e.g. for special needs in a different project. Nevertheless, the intention to create a component shall always be as generic as it makes sense so that they can be used in many other projects. Components can be shared via NPM or bower packages and have access to all functionality a smallstack client already has.

## Usage
Smallstack components can be used in our Backoffice  & Nativescript Applications to plug pages together, comparable to a CMS on steroids. They can also be used in html pages directly, for example, to combine some components to one component.

## Technology
The smallstack framework provides a useful base for all components, including technology agnostic base classes that can be extended as well as an event system for the communication between components and the client itself. On top of that there are extendable base classes for Angular, Angular 2 and React. It is possible to combine components that are written in any UI technology.

## Communication
All components can access the smallstack service layer directly to load and modify data, as well as all raw Meteor functionality. A component also has input and output sockets where data can be sent or received with. This is useful to communicate with other components on a page without having to know who the sender or receiver is. These communication links can be created in the smallstack page builder, in the source code or directly inside the html code.

## Data
A component has its private data storage. If a component is stored inside a page model, that data is stored in the database, otherwise it is handled dynamically. The data storage can be prefilled with the component configuration (see below) by using the page builder and/or the helper methods on the related base classes.

## Configuration
With the component configuration an end customer can customize a component. The component configuration can be adjusted for each component via the page builder.

## Sockets
Component sockets are the easiest way to communicate with other components. A component can define input and output sockets together with their expected type. Connections between two sockets can be established via the page builder or the source code directly.

## How-to create a simple Angular Component
A minimal Angular Component exists of a html and a js|ts file. The AngularComponent factory class should be used to create and register a component. It also provides helper methods for adding meta data, component configuration and component sockets. In this example we create a component that shows a name that is preconfigured as component configuration:

### Folder Structure
If you're using Meteor its best to put all components into a subfolder of the famous "imports" folder, see docs.meteor.com, e.G.:
`/meteor/client/imports/components`


#### HTML Markup
Inside our smallstack project we create a file called HelloDave.html and add the following html markup: 
```
<div>Hello {{name}}</div>
```

#### Controller Class
Right next to the HTML file we can create a JS/TS file which can act as Controller. Create a controller class named hellodave.ts and add the business logic, for example: 
```
import { AngularComponent, AngularBaseComponentController } from "@smallstack/core-client";
import { ComponentConfiguration, InitializationAware } from "@smallstack/core-common";

import template from "./HelloDave.html";

export class HelloDaveComponent extends AngularBaseComponentController implements InitializationAware {

    public afterInitialization() {
        this.syncDataIfAvailable("name");
    }

}

AngularComponent.new("HelloDaveComponent", HelloDaveComponent)
    .setTemplate(template)
    .addConfiguration(ComponentConfiguration.createStringConfiguration("name", "Dave"))
    .register();
```

#### Run the example component
After creating a new component all you have to do is to import the file somewhere, e.g. in your meteor/client/index.ts. The "AngularComponent" factory will take care of registering the component in the AngularRootModule. You can then use your component in other HTML files by typing `<HelloDaveComponent></HelloDaveComponent>`.