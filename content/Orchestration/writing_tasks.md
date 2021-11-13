# Writing Tasks

[INDEX](../../README.md)

## Overview:
Tasks are kept in modules and can have metadata in order to share them. Can be writen in any programming language (Bash, PS, python, etc) and also can be compiled to run on targets.

### Naming tasks:

1. The name of the module where the task is located.
2. The name of the task file, without the extension.

For example, in the puppetlabs/mysql module, the sql task is located at ./mysql/tasks/sql.rb, so the task name is mysql::sql.

### Tasks metadata:
Describe task parameters, validate input, and control how Bolt executes the task. Naming convention <TASKNAME>.json inside ./tasks directory along with taks file.

```json
    {
    "description": "Allows you to execute arbitrary SQL",
    "input_method": "stdin",
    "parameters": {
        "database": {
            "description": "Database to connect to",
            "type": "Optional[String[1]]"   -> validation
        },
        "user": {
            "description": "The user",
            "type": "Optional[String[1]]"
        },
        "password": {
            "description": "The password",
            "type": "Optional[String[1]]",
            "sensitive": true   -> values are masked in logs
        },
        "sql": {
            "description": "The SQL you want to execute",
            "type": "String[1]"
        }
    }
    }
```

### Parameters:
Add prefix PT_ to variables inside the script/program.

```bash
    #!/usr/bin/env bash
    echo your message is $PT_message   # message=hello
```
