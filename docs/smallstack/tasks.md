# Tasks
In smallstack, "tasks" are repeatable chunks of source code with a friendly name. They can be executed manually via the "Tasks Backoffice" or via the "TaskRegistry" in your source code. An execution of a task leads to a "Task Execution" instance which holds all data being used for the execution as well as logs and some audit stuff. 

Tasks have full access to all smallstack services and all data. Tasks can be run concurrent or explicitly sequential.

Each task can define a required user role which will be checked upon execution.

# Task Execution
Task Executions are stored next to the tasks in your MongoDB. You can view them in the "Task Executions Backoffice" or query them via the related TaskExecutionService. Every each execution object holds some metadata like the context, the executor (human or system), the time, the logs and so on.

# Cronjobs
smallstack cronjobs are built upon our tasks system. Every execution of a cronjob will result in a new task execution object. Be aware of that creating cronjobs requires the same role as the to be executed task!

### A note about clusters
To avoid that many nodes execute the same cronjob simultaniously, you have to pick one node and set the environment variable CRONJOB_SCHEDULING to true, even in a one node system. This node then executes all cronjobs for you. If you have a lot of work to do it might make sense to start a dedicated node for cronjobs. If you are looking for different options, don't hesitate to ask for support!
