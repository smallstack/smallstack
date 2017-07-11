# Workflow Engine
The workflow engine in the smallstack framework is a simple but powerful event machine that is based on 3 particular base classes: events, conditions and actions. 

## How does the engine work?
A workflow has events, conditions and actions attached. If a specific event is fired, the WorkflowManager looks for workflows that have that event attached, checks its conditions and, if all are true, executes all actions. Events are "or", conditions and actions are "and".


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
