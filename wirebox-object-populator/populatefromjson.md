# populateFromJSON

Populate a bean from a JSON string

## Returns

* This function returns any

## Arguments

| Key | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| target | any | Yes | --- | The target to populate |
| JSONString | string | Yes | --- | The JSON string to populate the object with. It has to be valid JSON and also a structure with name-key value pairs. |
| scope | string | No |  | Use scope injection instead of setters population. Ex: scope=variables.instance. |
| trustedSetter | boolean | No | false | If set to true, the setter method will be called even if it does not exist in the bean |
| include | string | No |  | A list of keys to include in the population |
| exclude | string | No |  | A list of keys to include in the population |
| ignoreEmpty | boolean | No | false | Ignore empty values on populations, great for ORM population |
| nullEmptyInclude | string | No |  | A list of keys to NULL when empty |
| nullEmptyExclude | string | No |  | A list of keys to NOT NULL when empty |
| composeRelationships | boolean | No | false | Automatically attempt to compose relationships from memento |

