# parcel-typescript-validator-broken

This repo illustrates [an issue](https://github.com/parcel-bundler/parcel/issues/6779) `@parcel/validator-typescript`` `2.0.0-rc.0` where it will fail with typescript `4.4.2`. There is no issue with typescript `4.3.5`.

## Repro steps

1. Clone the repo and run `yarn` to install dependencies
2. Note the key parts of the configuration. All these must be present to see the issue:
  - typescript `4.4.2`.
  - a custom `tsconfig.json` present in the project.
  - `.parcelrc` configured to run `@parcel/validator-typescript`.
3. Run `yarn build`

### Result

Build fails with this output:

```
yarn run v1.22.11
$ parcel build src/index.html
🚨 Build failed.

@parcel/validator-typescript: directoryExists is not a function

  TypeError: directoryExists is not a function
  at Object.matchFiles (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/typescript/lib/typescript.js:20102:17)
  at ParseConfigHost.readDirectory (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/@parcel/ts-utils/lib/FSHost.js:105:20)
  at getFileNamesFromConfigSpecs (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/typescript/lib/typescript.js:40747:40)
  at getFileNames (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/typescript/lib/typescript.js:40250:29)
  at parseJsonConfigFileContentWorker
  (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/typescript/lib/typescript.js:40183:24)
  at Object.parseJsonConfigFileContent
  (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/typescript/lib/typescript.js:40124:16)
  at tryCreateLanguageService
  (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/@parcel/validator-typescript/lib/TypeScriptValidator.js:138:53)
  at /Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/@parcel/validator-typescript/lib/TypeScriptValidator.js:87:7
  at async Promise.all (index 0)
  at async Object.validateAll
  (/Users/Andrew/Projects/parcel-typescript-validator-broken/node_modules/@parcel/validator-typescript/lib/TypeScriptValidator.js:81:5)
error Command failed with exit code 1.
```
