# Workflow Engine
The workflow engine in the smallstack framework is a simple but powerful event machine that is based on 3 particular base classes: events, conditions and actions. 

## How does the engine work?
A workflow has events, conditions and actions attached. If a specific event is fired, the WorkflowManager looks for workflows that have that event attached, checks its conditions and, if all are true, executes all actions.

### Events
Events are strings that can be fired from everywhere. An event fired on a client will not trigger any workflows on the server and vice versa. If multiple events are attached to a workflow, one alone will trigger the workflow (like a logical "or").

#### Example Events
* Startup
* User registers
* Payment done
* Something happened in a native application

### Conditions
Conditions can access the current workflow context and all other services in their environment. If a workflow has multiple conditions attached, it will not get executed if one of them fails (logical "and"). If you wish to explicitly do a logical "or", please use the ORCondition class.

#### Example Conditions
* Time
* Weather
* context related stuff like user profile conditions

### Actions
An action can be a Task (see tasks documentation) or any other implementation of the WorkflowAction interface. Even firing an event can be an action. If multiple actions are attached to a workflow, all actions are executed in sequence, no matter if one fails (an absolute logical "and")

#### Example Actions
* Execute Task
* Send a mail
* Deactivate a user
* Fire Event Action

## Example
```typescript
// Action
export class ConsoleGreetingAction extends WorkflowAction {
    public execute(): void {
        Logger.info("ConsoleGreeting", "This is a greeting message from the brand new workflow engine! See https://github.com/smallstack/smallstack/blob/master/docs/general/workflows.md for more details!");
    }
}

// Event
export class StartupEvent extends WorkflowEvent {
    constructor() {
        super();
        Meteor.startup(() => {
            this.fire();
        });
    }
}

// Workflow
const workflow: Workflow = Workflow.fromDocument<Workflow>({
    events: ["StartupEvent"],
    actions: ["ConsoleGreetingAction"]
});

// Register all objects
IOC.onRegister("workflowManager", (workflowManager: WorkflowManager) => {
    workflowManager.registerWorkflowAction(new ConsoleGreetingAction());
    workflowManager.registerWorkflowEvent(new StartupEvent());   
    workflowManager.registerWorkflow(workflow);
});

```
