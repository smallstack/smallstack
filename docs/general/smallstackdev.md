# How-to develop on the smallstack stack

The stack itself doesn't run without a project. So either you use an already created project like https://github.com/smallstack/project-cocktailbar or you create an empty one as described here: https://github.com/smallstack/smallstack/blob/master/docs/general/projectcreation.md (not recommended right now).

1. Install all prerequisites, see https://github.com/smallstack/smallstack/blob/master/docs/general/install.md
2. Checkout the smallstack repository from https://bitbucket.org/smallstack/smallstack.git
3. Call `smallstack setup` in the root folder of your smallstack framework checkout. This will link the smallstack modules to their dependent modules and install NPM dependencies
4. Call `smallstack generate` in the root folder to generate all sources for all types (see https://github.com/smallstack/smallstack/blob/master/docs/general/datalayer.md &&  https://github.com/smallstack/smallstack/blob/master/docs/general/types.md)
5. Call `smallstack bundle` which will initially bundle all sources so that they can be used by projects.
6. Open a new command prompt and go to a project of your choice
7. Call `smallstack setup` and choose the local checkout mode. Please provide a relative path to the root folder of your smallstack framework checkout.
8. (optional) Go back to the smallstack framework prompt and call `smallstack watch` to watch all changes. This will recompile the related module if you change sources. If you change the typesystem (e.g. a \*.smallstack.json file) you have to stop your meteor server, stop this watch and do a fresh `smallstack clean generate bundle` as well as a `smallstack generate` in your project.

## Tips & Tricks
### Typesystem / Datalayer changes
Whenever you change the typesystem in the smallstack framework, you have to call `smallstack clean generate bundle` in the framework root and `smallstack generate` in the project root.

### Folder Structure
In a workspace directory, lets call it \home\users\max\ws, the easiest way to work with several smallstack projects and the framework together is, to put them all on the same level, e.g.:

\home\users\max\ws\smallstack

\home\users\max\ws\project-cuppy

\home\users\max\ws\project-urbanpacman


That way, most of the times, you can just hit "enter" in the CLI if you get asked for relative paths.
