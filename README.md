# NOTE

*This a fork from a fork, see GitHub. It will probably be stripped down to mere basics, e.g. removing event listening API. Below information might be or become obsolete.*

# Avanza-lib

A Node.js wrapper for the unofficial Avanza API. Please note that this is only a proof of concept, hence not meant to be used by anyone.

## Installation

Install via [npm](https://www.npmjs.com/package/@g71/avanza-lib)
```bash
$ npm install @g71/avanza-lib
```
## Documentation

Refer to [API.md](./API.md).

## Getting a TOTP Secret

Here are the steps to get your TOTP Secret:

0. Go to Profil > Inställningar > Sajtinställningar > Inloggning och utloggning > Användarnamn > Tvåfaktorsinloggning and click "Återaktivera". (Only do this step if you have already set up two-factor auth.)
1. Click "Aktivera" on the next screen.
2. Select "Annan app för tvåfaktorsinloggning".
3. Click "Kan du inte scanna QR-koden?" to reveal your TOTP Secret.
5. Finally, run `node -e "console.log(require('avanza-lib/dist/totp')('PASTE_YOUR_TOTP_SECRET_HERE'))"` to generate an initial code.
6. Done! From now on all you have to do is supply your secret in the `authenticate()` function as in the example below.

## Example

Authenticate and fetch currently held positions:

```javascript
import Avanza from 'avanza-lib'
const avanza = new Avanza()

avanza.authenticate({
  username: 'MY_USERNAME',
  password: 'MY_PASSWORD',
  totpSecret: 'MY_TOTP_SECRET'
}).then(async () => {
  const positions = await avanza.getPositions()
  console.log(positions)
})
```

Authenticate and subscribe to real-time data:

```javascript
import Avanza from 'avanza-lib'
const avanza = new Avanza()

avanza.authenticate({
  username: 'USERNAME',
  password: 'PASSWORD',
  totpSecret: 'MY_TOTP_SECRET'
}).then(() => {
  avanza.subscribe(Avanza.QUOTES, '5479', (quote) => {
    console.log('Received quote:', quote)
  })
})
```
## Documentation

Refer to [API.md](API.md).

## Tests

Tests will not run without an `.env` file. Use the `.env-example` as reference.

```bash
$ npm test
```
## LICENSE

MIT license. See the LICENSE file for details.

## RESPONSIBILITIES

The author of this software is not responsible for any indirect damages (foreseeable or unforeseeable), such as, if necessary, loss or alteration of or fraudulent access to data, accidental transmission of viruses or of any other harmful element, loss of profits or opportunities, the cost of replacement goods and services or the attitude and behavior of a third party.
