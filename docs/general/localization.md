# Localization
The smallstack framework supports different ways of storing a localization

## Via Sourcecode
Localization files are a great way to store initial or cross-project localization in a versionized sourcecode. The smallstack framework supports 2 ways of localization files: Client-side only and server-side. 

### server-side via sourcecode
Server-side localization gets loaded during server startup and will then get imported into the database. It will get tagged with `origin:code`. 

### client-side via sourcecode
Client-side localization gets loaded on the client only and will never get synced into the database. It will get tagged with `origin:clientOnly`. 

## Via Backoffice
All serverside localization will also show up in the I18N Backoffice. To prevent a server restart to override your dynamic modifications you've done via the backoffice, all localizations that were created or updated will get tagged with `origin:backoffice`

## Override order
Backoffice localizations overrule clientOnly and code localizations. 
