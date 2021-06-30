spare-Api
======

## Usage example

```js
const { readFileSync } = require('fs');
const { Connection, constants, ApiClient } = require('spare-api');

(async () => {
  const conn = new Connection('localhost:55400', {
    cert: readFileSync('private_daemon.crt'),
    key: readFileSync('private_daemon.key'),
  });
  conn.onMessage((message) => {
    console.log(message);
  });
  conn.addService(constants.SERVICE.walletUi);
  const fullNode = new ApiClient.FullNode({ connection: conn, origin: 'my-cool-service' });
  await fullNode.init();
  const blockchainState = await fullNode.getBlockchainState();
})();
```
