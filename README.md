# Cypress MetaMask

This plugin is based on the solutions brought by [Jakub Mucha - drptbl](https://github.com/drptbl) in [Synpress](https://github.com/Synthetixio/synpress), but with a more stripped down and (this is opinionated) simpler approach. The goal is to build a fairly straight forward solution that you can integrate into your own testing (end-to-end) flow.

Forked from - [cypress-metamask](https://github.com/CraftAcademyLabs/cypress-metamask)

### Setup
Install the package using `yarn` or `npm`:

```bash
$ yarn add -D cypress-web3-plugin
// or 
$ npm i -D cypress-web3-plugin
```

Import the plugin in `cypress/support/index.js` 

```js
// Import commands.js using ES2015 syntax:
import './commands'
import 'cypress-web3-plugin'
```

Modify your `cypress/plugins/index.js` to include the plugin:

```js
module.exports = (on, config) => {
  require('cypress-web3-plugin/cypress/plugins')(on)
}
```

Add an `.env` file to your project root:

```
SECRET_WORDS="test test test test test test test test test test test junk"
PASSWORD=TestMetaMask
METAMASK_VERSION=latest 
NETWORK_NAME=BSC 
RPC_URL=https://bsc-dataseed.binance.org/
CHAIN_ID=56
```

Add these scripts to your `package.json` (or modify your existing scripts): 

```json
"e2e": "cross-env CYPRESS_REMOTE_DEBUGGING_PORT=9222 cypress open"
```

**You should be ready to go.** 

## Example

```js
describe('User can load page', () => {
  before(() => {
    cy.setupMetamask();
    cy.changeMetamaskNetwork('localhost')
    cy.visit('/')
  });
  it('is expected to display a sussess message', () => {
    cy.get('[data-cy=title]').should('contain.text', 'MetaMask Detected')
  });
  
  it('is expected to display the local wallet address', () => {
    cy.get('[data-cy=address').should('contain.text', 'Your address is: 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266')
  });
  
  it('is expected to display the local wallet  balance', () => {
    cy.get('[data-cy=balance').should('contain.text', 'Balance: 10000000000000000000000')
  });
})
```



