# Cypress
[Cypress](cypress.io) is a Javascript End to End testing framework.

## IDE Setup
For VS Code, add a triple-slash directive to the head of your JavaScript or TypeScript testing file. This will turn the IntelliSense on a per file basis.

```xml
/// <reference types="Cypress" />
```

## Commands

### Test structure

```js
describe('My Test Name', function() {
  before(() => {
    // Things to do before the first test
  })

  beforeEach(() => {
    // Things to do before every test
  })

  it('My Subtest', function() {
    // Your test here
  })
});
```

### Selecting elements
```js
// Based on CSS class
cy.get('.myClass');
// Based on ID
cy.get('#myID');
// Based on element properties
cy.get('[name=username]')
// Based on element type and properties
cy.get('input[name=username]')

// Based on contents
cy.contains('name')
// Get + Contains
cy.contains(selector, text)   // get(selector).contains(text)

// Alias
cy.get('...')
  .as('item')
// Then we can use it as:
cy.get('@item')

// Element under focus
cy.focused();

// Cookies
cy.getCookie('your-session-cookie')
```


### Interacting with the page

```js
// Visit a webpage
cy.visit(url)

// Enter text to an input field
.type('text')
// Pass a sequence
.type('{leftarrow}{enter}{esc}')

// Perform click
.click()

/* URL opearations */
// Check if URL includes a string
cy.url().should('include', '/commands/actions');
```

### Debugging Commands

__Pause__

Pause test execution.

```js
cy.pause();
cy.pause().getCookie('app') // Pause at the beginning of commands
cy.get('nav').pause();       // Pause after the 'get' commands yield
```

__Debug__

Set a debugger and log what the previous command yields. 
You need to have your Developer Tools open for `.debug()` to hit the breakpoint.

```js
cy.debug().getCookie('app') // Pause to debug at beginning of commands
cy.get('nav').debug();      // Debug what the `get` command yields
```

### Assertions
Assertions can be performed using `.should(verb[, expression])`, which has a verb that interacts with an optional expression.

Verbs:

```js
contain         // Check text contents of the item and its children
include         // Equivalent to 'contain'
have.value      // cy.get('.email').should('have.value', 'mail@email.com');
have.class      // cy.get('item').should('have.class', 'myClass')
exist           // cy.get('item').should('exist')
not.exist       // cy.get('item').should('not.exist')
```

### Custom Commands
Cypress allows creating custom commands and overwriting existing commands. It is recommended that they are placed in `cypress/support/commands.js`, since it is loaded before any test files.

```js
// Syntax
Cypress.Commands.add(name, callbackFn)
Cypress.Commands.add(name, options, callbackFn)
Cypress.Commands.overwrite(name, callbackFn)
Cypress.Commands.overwrite(name, options, callbackFn)

// Example
Cypress.Commands.add('login', (email, pw) => {})

// Usage
cy.login('admin', 'myPass');
```
