# Purpose 
If you use the smallstack types (see https://github.com/smallstack/smallstack/blob/master/docs/general/types.md) you automatically get a layer of services and models generated, we call that layer "datalayer" (very catchy name, heh...)

The Datalayer has some advantages:
* It can be used on the server, in browsers and nativescript applications at the same time (one source)
* It is technology agnostic, meaning, its not bound to any framework, even not to smallstack
* It takes care of how to get data from the database to the clients, in a secured way
* Based on the datalayer, we can generate UI components and use smallstack components in a generic way (e.g. use the ListComponent for any type) 


# smallstack query language
The smallstack query language (SQL, right?) translates your configured types into service methods which can be executed on clients and on servers. On clients it also takes care of subscribing to the related publications and the syncing to the clients local mongoDB instance. Here's an example


```
export class TaskExecutionBackoffice extends Angular2BaseComponentController {

    public executions: TaskExecution[];

    @Autowired()
    private taskExecutionsService: TaskExecutionsService;

    public loadExecution(id: string) {
        this.taskExecutionsService.getTaskExecutionById({ id }, { reactive: true }).subscribe((error: Error, queryObject: QueryObject<TaskExecution>) => {
            Tracker.autorun(() => {
                const executions: TaskExecution[] = queryObject.getModels();
                this.ngZone.run(() => {
                    this.executions = executions;
                });
            });
        });
    }
}
```
Notes:
* reactive: true tells the query language that the subscription should be reactive and re-run if a model in the database changes
* Tracker.autorun is Meteor Functionality and takes care of re-running a block if block-level properties have changed, see https://docs.meteor.com/api/tracker.html
* NGZone.run is Angular4 Functionality and takes care of syncing local data that has been changed inside async blocks

The QueryObject has a pretty forward set of methods:
* getModels(callback?: (models: ModelClass[]) => void): ModelClass[];
* getModel(index: number, callback?: (model: ModelClass) => void): ModelClass;
* subscribe(onReadyCallback?: (error: Error, queryObject: QueryObject<ModelClass>) => void): void;
* expand(foreignKeys: string[], callback?: () => void): void;
* getCount(callback: (count: number) => void): void;
* getPage(pageNumber: number, callback: (models: ModelClass[]) => void): void;
* getNextPage(callback: (models: ModelClass[]) => void): void;
* getCurrentPage(callback: (models: ModelClass[]) => void): void;
* getPreviousPage(callback: (models: ModelClass[]) => void): void;
* hasNextPage(): boolean;
* hasPreviousPage(): boolean;


# Security
All data is public by default, this is by design. If you want to restrict data being published, you have to change the MongoDB Selectors, e.g. to only select models where owner ID is equal to the users ID. Or you use accessors, which are a more programmatic way of selecting documents.
