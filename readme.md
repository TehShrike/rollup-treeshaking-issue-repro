# Rollup treeshaking issue repo

tl;dr: Rollup's treeshaking can produce invalid JS syntax.

## To reproduce

```sh
npm it
```

- installs Rollup
- runs Rollup with the included [`./rollup.config.js`](./rollup.config.js) file
- runs the output with node

### Expected behavior

There should be no syntax files in the output

### Observed behavior

There is a syntax error caused by removing an irrelevant expression before a comma operator.

## Other notes

Setting `treeshake: false` in the Rollup config and running the build will produce valid syntax.

I ran into this issue in an app that needs to import `@auth0/auth0-spa-js`, which contains this kind of code (search <https://unpkg.com/@auth0/auth0-spa-js@1.3.0/dist/auth0-spa-js.production.js> for "`for(Be in!0`").
