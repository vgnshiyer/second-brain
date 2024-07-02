Created on 2024-07-01_21-03-19

## 📔 Notes

- Rego is a declarative language for defining policies.
- In rego, policies begin with a head.
- The expressions are evaluated one by one to determine if the policy is true or false.
- The policy is true if all the expressions are true.

For example:
```rego
package example

default allow = false

allow { # head
    input.method == "GET" # expression 1
    input.path == ["data", "foo"] # expression 2
}
```

- The above policy is true if the method is GET and the path is `data/foo`.
- The `default` keyword is used to set the default value of the policy.
- The `input` keyword is used to access the input data.
- The `package` keyword is used to define the package name.

### Functions

- Functions are used to define reusable expressions.
- Functions are defined using the `function` keyword.
- Functions can be called using the function name.

For example:
```rego
package example

default allow = false

allow {
    input.method == "GET"
    input.path == ["data", "foo"]
    is_admin(input.user)
}

is_admin(user) {
    user == "admin"
}
```

- The above policy is true if the method is GET, the path is `data/foo`, and the user is `admin`.

### Rules

- Rules are used to define reusable policies.
- Rules are defined using the `rule` keyword.
- Rules can be called using the rule name.

For example:
```rego
package example

default allow = false

allow {
    input.method == "GET"
    input.path == ["data", "foo"]
    is_admin(input.user)
}

is_admin(user) {
    user == "admin"
}

rule allow_admin {
    allow
}
```

- The above policy is true if the method is GET, the path is `data/foo`, the user is `admin`, and the `allow_admin` rule is true.

### Imports

- Imports are used to import external policies, functions, and rules.
- Imports are defined using the `import` keyword.

For example:
```rego
package example

import data.example

default allow = false

allow {
    input.method == "GET"
    input.path == ["data", "foo"]
    is_admin(input.user)
}

is_admin(user) {
    user == "admin"
}

rule allow_admin {
    allow
}
```

- The above policy imports the `example` package from the `data` module.

### Data

- Data is used to define input data.

For example:
```rego
package example

default allow = false

input = {
    "method": "GET",
    "path": ["data", "foo"],
    "user": "admin"
}

allow {
    input.method == "GET"
    input.path == ["data", "foo"]
    is_admin(input.user)
}

is_admin(user) {
    user == "admin"
}

rule allow_admin {
    allow
}
```

- The above policy defines the input data using the `input` keyword.

### Testing

- Rego policies can be tested using the `test` keyword.

For example:
```rego
package example

default allow = false

input = {
    "method": "GET",
    "path": ["data", "foo"],
    "user": "admin"
}

allow {
    input.method == "GET"
    input.path == ["data", "foo"]
    is_admin(input.user)
}

is_admin(user) {
    user == "admin"
}

rule allow_admin {
    allow
}

test allow {
    allow with input as input
}

test is_admin {
    is_admin("admin")
}

test allow_admin {
    allow_admin
}
```

- The above policy defines three tests for the `allow`, `is_admin`, and `allow_admin` rules.

## 🔗 Links

- [[]]
