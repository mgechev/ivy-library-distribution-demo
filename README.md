# Ivy Library Distribution Demo

**This project focuses on low-level technical details, which are transparent for application and library developers**. If you're interested in giving a try of the new library distribution mechanism, read the content below and follow the external references. If not, ignore this project and wait until we enable this in a future version. We're expecting significant build time and postinstall improvements 🔥.

## Details

This workspace shows a sample usage of the **experimental** Angular linker used for library distribution. The only difference from a standard Angular project is in `tsconfig.lib.prod.json`, which now contains an extra flag under `angularCompilerOptions` and sets the `enableIvy` property to `true`:

```js
/* To learn more about this file see: https://angular.io/config/tsconfig. */
{
  "extends": "./tsconfig.lib.json",
  "compilerOptions": {
    "declarationMap": false
  },
  "angularCompilerOptions": {
    "enableIvy": true,
    "compilationMode": "partial"
  }
}
```

## Background

As part of our migration from View Engine to Ivy we have a couple of major efforts. One of them is to figure out the library distribution strategy. In the previous versions of the Angular compiler we used to resolve the metadata for the Angular libraries in the project using `metadata.json` files and we encouraged. Because of the locality principle in Ivy and build performance concerns, we took a different direction which we listed in [this RFC](https://github.com/angular/angular/issues/38366).

As part of the new mechanism Angular CLI will now "partially compile" libraries and prepare them for distribution to package registries. Later on, when developers install a library in their project we'll use the Angular linker to transform the partially compiled form to Ivy instructions.

## License

MIT
