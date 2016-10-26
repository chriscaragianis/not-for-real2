# creative-lambdas

## Using the scripts

### Build a new lambda

```zsh make_service.sh <name-of-service>```

This looks in the `templates` directory and creates boilerplate. For example:

```zsh make_service.sh newLambda```

produces

```
├── newLambda
│   ├── .babelrc
│   ├── .env
│   ├── .eslintrc
│   ├── dist
│   │   ├── .env
│   │   ├── context.json
│   │   ├── deploy.json
│   │   └── event.json
|   |
|   |  (node_modules hidden)
|   |
│   ├── package.json
│   └── src
│       ├── fixtures
│       │   ├── fakeContext.js
│       │   └── fakeEvent.js
│       ├── index.js
│       └── test
│           └── index.test.js`
```
Note that `deploy.env` and `.env` are copied from a `templates/hidden`
directory not checked in. See [ node-lambda ]( https://www.npmjs.com/package/node-lambda ) for more information.

### Testing

#### Unit tests

Unit tests are set up to import the `fakeEvent.js` and `fakeContext.js`
files.  Running `npm test` will

  * lint the project according to your `.eslintrc`
  * build the project into `dist/`
  * run all tests found in `dist/test`

#### Lambda test run

Running `node-lambda run` in `dist` will run your lambda as though triggered
with the message found in `dist/event.json` and with any extra contextual data
found in `dist/context.json`. The run will output the object passed to either the `context.succeed()`
or `context.fail()` function. See [ node-lambda ]( https://www.npmjs.com/package/node-lambda ) for more information.

#### Integration testing

The `integrations.sh` script is an example of a local test of a chain of lambda
functions. Using `output_cleaner.rb` we can log the output of one lambda to the
`event.json` of the next. (WIP).


