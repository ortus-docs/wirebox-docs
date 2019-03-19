# populateFromQueryWithPrefix

Populates an Object using only specific columns from a query. Useful for performing a query with joins that needs to populate multiple objects.

## Returns

* This function returns any

## Arguments

The structure to populate the object with.

| Key | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| target | any | Yes | --- | This can be an instantiated bean object or a bean instantiation path as a string. If you pass an instantiation path and the bean has an 'init' method. It will be executed. This method follows the bean contract \(set{property\_name}\). Example: setUsername\(\), setfname\(\) |
| qry | query | yes | --- | The query to populate the bean object with |
| rowNumber | Numeric | No | 1 | The query row number to use for population |
| scope | string | No |  | Use scope injection instead of setters population. Ex: scope=variables.instance. |
| trustedSetter | boolean | No | false | If set to true, the setter method will be called even if it does not exist in the bean |
| include | string | No |  | A list of keys to include in the population |
| exclude | string | No |  | A list of keys to include in the population |
| prefix | string | Yes | --- | The prefix used to filter, Example: 'user\_' would apply to the following columns: 'user\_id' and 'user\_name' but not 'address\_id'. |
| ignoreEmpty | boolean | No | false | Ignore empty values on populations, great for ORM population |
| nullEmptyInclude | string | No |  | A list of keys to NULL when empty |
| nullEmptyExclude | string | No |  | A list of keys to NOT NULL when empty |
| composeRelationships | boolean | No | false | Automatically attempt to compose relationships from memento |

