# Validate incoming objects against Swagger Models for Node.js

[ ![Codeship Status for atlantishealthcare/swagger-model-validator](https://codeship.io/projects/a4ec3310-3b9b-0132-060c-1e7e00028aa9/status)](https://codeship.io/projects/42728)

This is a validation module for [Swagger](https://github.com/wordnik/swagger-spec) models Node.js.

See the [swagger-node-express](https://github.com/wordnik/swagger-node-express/blob/master/SAMPLE.md) sample for more details about Swagger in Node.js.

## What's Swagger?

The goal of Swagger™ is to define a standard, language-agnostic interface to REST APIs which allows both humans and computers to discover and understand the capabilities of the service without access to source code, documentation, or through network traffic inspection. When properly defined via Swagger, a consumer can understand and interact with the remote service with a minimal amount of implementation logic. Similar to what interfaces have done for lower-level programming, Swager removes the guesswork in calling the service.

Check out [Swagger-Spec](https://github.com/wordnik/swagger-spec) for additional information about the Swagger project, including additional libraries with support for other languages and more. 

## Validating Swagger Models?

A Swagger Model contains the definitions of the incoming (or outgoing) object properties.  Validating an incoming object matches the Swagger Model Definition is a valuable check that the correct data has been provided.

This package provides a module to do just that.

### Limitations
This edition of the swagger-model-validator will not validate models referenced in a model by the $ref keyword.  
It will also not validate arrays (either arrays of objects or strings, integers, etc...)

It currently treats int32 and int64 the same.
It currently treats float and decimal the same.
It currently treats date and date-time the same.

It is planned that it will validate everything correctly as time allows.

### Installation
Install swagger-model-validator

```
npm install swagger-model-validator
```

Create a validator and pass your swagger client into it.
```
var Validator = require('swagger-model-validator');
var validator = new Validator(swagger);
```

Now you can call validateModel on swagger to validate an incoming json object.

```
var validation = swagger.validateModel("modelName", jsonObject);
```

This returns a validation results object

```
{
  valid: true,
  errorCount: 0
}
```
or if validation fails
```
{
  valid: false,
  errorCount: 2,
  errors: [
    {
      name: 'Error',
      message: 'An error occurred'
    },
    {
      name: 'Error',
      message: 'Another error occurred'
    }
  ]
}
```

You can also call the validation directly

```
var validation = validator.validate(object, swaggerModel);
```

will return the same validation results but requires the actual swagger model and not its name.

## License

Copyright (c) 2014 Atlantis Healthcare Limited.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
