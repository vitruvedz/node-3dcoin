# node-3dcoin
[![npm][npm-image]][npm-url]
[![downloads][downloads-image]][downloads-url]
[![js-standard-style][standard-image]][standard-url]


[npm-image]: https://img.shields.io/npm/v/3dcoin.svg?style=flat
[npm-url]: https://npmjs.org/package/3dcoin

[downloads-image]: https://img.shields.io/npm/dm/3dcoin.svg?style=flat
[downloads-url]: https://npmjs.org/package/3dcoin

[standard-image]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat
[standard-url]: http://standardjs.com

node-3dcoin is a simple wrapper for the 3dcoin client's JSON-RPC API.

The API is equivalent to the API document [here](https://en.bitcoin.it/wiki/Original_Bitcoin_client/API_Calls_list).
The methods are exposed as lower camelcase methods on the `3dcoin.Client`
object, or you may call the API directly using the `cmd` method.

## Install

`npm i 3dcoin`

## Examples

### Create client
```js
// all config options are optional
var client = new node_3dcoin.Client({
  host: 'localhost',
  port: 'port',
  user: 'username',
  pass: 'password',
  timeout: 30000
});
```

### Get balance across all accounts with minimum confirmations of 6

```js
client.getBalance('*', 6, function(err, balance, resHeaders) {
  if (err) return console.log(err);
  console.log('Balance:', balance);
});
```
### Getting the balance directly using `cmd`

```js
client.cmd('getbalance', '*', 6, function(err, balance, resHeaders){
  if (err) return console.log(err);
  console.log('Balance:', balance);
});
```

### Batch multiple RPC calls into single HTTP request

```js
var batch = [];
for (var i = 0; i < 10; ++i) {
  batch.push({
    method: 'getnewaddress',
    params: ['myaccount']
  });
}
client.cmd(batch, function(err, address, resHeaders) {
  if (err) return console.log(err);
  console.log('Address:', address);
});
```

