# What is a type
A smallstack type defines a collection of objects in a NoSQL database. It is stored in json files and used by the smallstack CLI to generate typescript class files. A smallstack type file generates a collection, a service and a model class on both the server and the client. The collection provides default access rules and basic access methods, the service handles the data aggregation and the model the property handling of each data object. 

# Do I need to use smallstack types?
Of course not. For almost all data commonly used in web projects they come in handy since they are generated, well tested and so easy to use. Sometimes it makes sense, sometimes not. Just create some types, extend them and see how you can use them. If you find it useful, use it, otherwise you can also use your own way of defining collections and how to deal with the data.

# How-to create a type
smallstack types are defined in json files. They are stored in {PROJECT_ROOT}\datalayer\types. A typical type can look like this: 

```
{
	"collection": {
		"name": "competitions"
	},
	"service": {
		"queries": [
			{
				"name": "getCompetitionByName",
				"selector": {
					"name": ":name:string"
				}
			}
		],
		"securedmethods": [
			{
				"name": "createCompetition",
				"parameters": [
					"competitionName:string",
					"competitionType:string"
				],
				"returns": "Competition"
			}
		]
	},
	"model": {
		"name": "Competition",
		"schema": [
			{
				"name": "ownerId",
				"type": "foreign",
				"collection": "users"
			},
			{
				"name": "name",
				"type": "string"
			},
			{
				"name": "type",
				"type": "string",
				"allowedValues": [
					"tournament",
					"league"
				]
			}
		]
	}
}
``` 

## Localization
You can localize a type by following this convention:

```
models.{{lower case model name}}.{{lower case schema field name}}.label|helptext|placeholder
```

So if you would like to localize the competition name from above, you could do:
```javascript
LocalizationService.instance().addTranslation(["en", "de"], {
    models: {
        competition: {
            name: {
                label: ["Competition", "Wettbewerb"],
		helptext: ["This is the name of your competition!", "Dies ist der Name deines Wettbewerbs!"],
		placeholder: ["A catchy name!", "Ein einprägsamer Name!"]
            }
        }
    }
});
```


## Generated files
This will create the following files:

### GeneratedCompetitionsCollection.ts
This file defines a collection called "competitions" on the server and the client. It is accessible via `smallstack.collections["competitions"]`. A slightly modified version of the famous SimpleSchema Meteor package is attached and filled with the model definition. It also creates a search index by using EasySearch and creates general getters and setters for the collection. This file should not get checked into SCM since it will be generated again when you hit `smallstack generate`.

### CompetitionsCollection.ts
This class is empty, extends GeneratedCompetitionsCollection and will be instanciated by the smallstack framework during startup. In this class you can modify the standard behaviour of the collection. This file can be checked into your SCM and will get eventual updates being made to the collection through the generated class `GeneratedCompetitionsCollection`.

### GeneratedCompetitionsService.ts
The generated service class provides the access to the collection. If you defined securedmethods or queries, then you can find them (or their helper methods) in this class, e.g. the query `getCompetitionById` from above. In addition it provides standard CRUD methods for saving, updating and deleting collection objects.

### CompetitionsService.ts
Just like the `CompetitionsCollection.ts` file this file is empty and can be used for your own needs. It extends the GeneratedCollectionService.

### GeneratedCompetition.ts
The generated model class has all properties with their types as public class properties. It provides related enums (e.g. for string types with allowed values), static object to domain model converter methods (fromDocument, toDocument), list type accessors and model related methods defined in the type json file as well as forwarded CRUD methods. If you load an object from a collection, it will be an instance of, in this case, `Competition`.

### Competition.ts
Extends the `GeneratedCompetition.ts` file and can be used for your own custom needs, e.g. for advanced model property getters or model related operations.
