# Usefull tricks

## Working with json

```python
import json

json_string = "{'test':1}"

# parse json
my_dictionnary = json.loads(json_string)
print(my_dictionnary['test'])
# output: 1

# stringify dictionnary to json
my_json_string = json.dumps(my_dictionnary)
print(my_json_string)
# will return something like json_string
