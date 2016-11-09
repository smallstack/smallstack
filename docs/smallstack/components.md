# Smallstack Components
A smallstack component is an isolated part of a website that can be reused across different pages or web projects. They can serve a UI,  fullfill some business logic or both. The smallstack framework already has a lot of components, but sometimes it is necessary to create new ones e.g. for special needs in a different project. Nevertheless, the intention to create a components shall always be as generic as it makes sense so that they can be used in many other projects. Components can be shared via NPM or bower packages and have access to all functionality a smallstack client already has.

## Usage
Smallstack components can be used in the smallstack page builder to plug pages together, comparable to a CMS on steroids. They can also be used in html pages directly, for exampl, to combine some components to one component.

## Technology
The smallstack framework provides a useful base for all components, including technology agnostic base classes that can be extended as well as an event system for the communication between components and the client itself. On top of that there are extendable base classes for Angular, Angular 2 and React. It is possible to combine components that are written in any UI technology.

## Communication
All components can access the smallstack service layer directly to load and modify data, as well as all raw Meteor functionality. A component also has input and output sockets where data can be sent or received with. This is useful to communicate with other components on a page without having to know who the sender or receiver is. These communication links can be created in the smallstack page builder, in the source code or directly inside the html code.

## Data
A component has its private data storage. If a component is stored inside a page model, that data is stored in the database, otherwise it is handled dynamically. The data storage can be prefilled with via the component configuration (see below) by using the page builder and/or the helper methods on the related base classes.

## Configuration
With the component configuration an end customer can customize a component. The component configuration can be adjusted for each component via the page builder.

## Sockets
Component sockets are the easiest way to communicate with other components. A component can define input and output sockets together with their expected type. Connections between two sockets can be established via the page builder or the source code directly.

## How-to create an Angular 1 component
A minimal Angular 1 component exists of a ng.html and a js|ts file. The AngularComponent factory class should be used to create and register a component. It also provides helper methods for adding meta data, component configuration and component sockets. In this example we create a component that shows a name that is preconfigured as component configuration:

#### HTML Markup
Inside your smallstack project create a file  called /client/components/hellodave/hellodave.ng.html and add the html markup: 
```
<div>Hello {{name}}</div>
```

#### Controller Class
Create a controller class named /client/components/hellodave/hellodave.ts and add the business logic, for example: 
```
class HelloDaveComponentController extends AngularBaseComponentController implements InitializationAware {

    public afterInitialization() {
        this.$scope.name = this.getData("name");
    }
    
}

AngularComponent.new("helloDave")
    .setControllerClass(HelloDaveComponentController)
    .setTemplateUrl('/client/components/hellodave/hellodave.ng.html')
    .setLabel("Hello Dave Example Component")
    .setDescription("A super useless component showing a name in a div!")
    .addConfiguration(ComponentConfiguration.createStringConfiguration("name", "Dave"))
    .create();
```

#### Run the example component
Since meteor automatically picks up all files this is all we have to do. After you compiled the source file with ```smallstack compile``` you should be able to see the component in the page builder. If you just want to display the component you can adjust an html file by adding ```<hello-dave></hello-dave>``` since components that are written in Angular 1 are actually just Angular Directives.
