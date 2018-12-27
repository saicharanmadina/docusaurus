---
id: doc2
title: Governance UI
---

The Ledgerium governance app UI

The governance UI is a NodeJS application using handlebars. To run it locally (assuming the dev environment setup is done as per https://github.com/ledgerium/LedgeriumWiki) run this after installing the dependencies. The governanceUI also expects the smart contract is up to date with latest bytecode and contract address.

Governance UI is a Dapps that works with Metamask for making signed transactions. Metamask has to be installed to use the governance app.

```
node governanceUI.js
```

The GovernanceUI is served default from port `3002`. Access `localhost:3002` from your browser.

All transactions have to be signed by the privatekey managed by the metamask plugin on the browser.

It is also important to note that certain actions will be restricted if the account is not an admin, admins or not are determined by the smartcontracts deployed initially. EOAs can be only validators without being an admin, they can participate in the voting/consensus rounds to votein/voteout other validators.