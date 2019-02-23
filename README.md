# postgraphile-log-consola

This [PostGraphile server
plugin](https://www.graphile.org/postgraphile/plugins/) disables
PostGraphile's query log and instead uses `consola` for logging.

## Installation

```
yarn add postgraphile-log-consola
```

## Usage - library

Use `makePluginHook` to load the plugin; see [the PostGraphile server plugins docs](https://www.graphile.org/postgraphile/plugins/) for more details.

```js
const { postgraphile, makePluginHook } = require("postgraphile");
const PostgraphileLogConsola = require("postgraphile-log-consola");

// Other server frameworks work similarly
const express = require("express");
const app = express();

const pluginHook = makePluginHook([PostgraphileLogConsola]); // 👈
app.use(
  postgraphile(process.env.DATABASE_URL, "public", {
    pluginHook, // 👈
    // ...
  })
);

app.listen(process.env.PORT || 3000);
```

## Usage - CLI

NOTE: `--plugins` must always be **the very first** option you use on the CLI.

Also note that this plugin only affects the query log, so the other messages the CLI generates are not wrapped.

```
postgraphile --plugins postgraphile-log-consola -c my_db
```
