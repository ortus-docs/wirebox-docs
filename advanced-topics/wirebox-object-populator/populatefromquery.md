# populateFromQuery

Populate a bean from a query

## Returns

 \* This function returns Any

## Arguments

| Key | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| target | any | Yes | --- | The target to populate |
| qry | query | yes | --- | The query to populate the bean object with |
| rowNumber | Numeric | No | 1 | The query row number to use for population |
| scope | string | No |  | Use scope injection instead of setters population. Ex: scope=variables.instance. |
| trustedSetter | boolean | No | false | If set to true, the setter method will be called even if it does not exist in the bean |
| include | string | No |  | A list of keys to include in the population |
| exclude | string | No |  | A list of keys to exclude in the population |
| ignoreEmpty | boolean | No | false | Ignore empty values on populations, great for ORM population |
| nullEmptyInclude | string | No |  | A list of keys to NULL when empty |
| nullEmptyExclude | string | No |  | A list of keys to NOT NULL when empty |
| composeRelationships | boolean | No | false | Automatically attempt to compose relationships from memento |

