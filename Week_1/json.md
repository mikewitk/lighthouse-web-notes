# npm and package.json

(NPM is Node's package manager)

## Packages
They are self-contained code libraries that we can install and use in our Node.js projects.

## Installing Packages

Say we want to install a packaged called **chalk**

*npm install chalk*

Done

## package.json

Virtually all Node.js projects have a file called **package.json**

## Installing a package

1. Create a directory to store the project.
  1. **Don't name the project with the same name of the package**
2. On terminal
  1. npm init
  2. Fillout the desired information
3. Next we need to install the package <NAME>. On terminal, type
  1. npm install --save <NAME>

`JSON`: JavaScript Object Notation

**Serialization** is the process that converts objects (or data structures) into a format that can be store or transmitted between computers.
**Deserialization** is the reverse process of `serialization`.

`JSON.parse()`
Parse a string as JSON, optionally transform the produced value and its properties, and retun the value.

`JSON.stringify()`
Return a JSON string corresponding to the specified value, optionally including only certain properties or replacing property values in a user-defined manner.