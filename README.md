# API Request & Response Runtime Validation

**Runtime** data validation of HTTP request & response body.

_For those who put too much trust in TypeScript_ ✨

## Install

```bash
npm install @safer-api/fetch

yarn add @safer-api/fetch
```

## Examples

### Path based validation

```ts
// `./src/fetch-safer.js`
import saferfetch from '@safer-api/fetch';

export const pathMapping = {
  `/api/user`: checkUserResponse,
  `/api/repos/`: checkRepoResponse,
  `GET /api/notes`: data => schema_id_and_note.parse(data),
  `POST /api/notes`: {
    request: (data) => schema_note.parse(data),
    response: (data) => schema_id_and_note.parse(data),
  }
};

export default saferfetch(pathMapping);
```

#### Usage

Use the module exported with `saferfetch(pathConfig)` just as you would `fetch(url, config)`.

```ts
import fetchSafer from './src/fetch-safer'

fetchSafer('/api/notes')
.then(response => {
  // Response is now validated based on any matching path rules passed into `saferfetch(pathMapping)`
})
.catch(error => {
  // If the validation function returns `false` or throws an `Error`, we can handle it here.
});
```
