## CSS AST explorer

**The ast explorer is not active since 2021/8/22, this fork just update postcss to the latest version for better debug experence**

Paste or drop css code into the editor and inspect the generated AST on https://postcss-rs.github.io/astexplorer/

The AST explorer provides following css parsers:

- [cssom][]
- [csstree][]
- [postcss][] + [postcss-safe-parser][] & [postcss-scss][]
- [rework][]

### Transforms

Since future syntax is supported, the AST explorer is a useful tool for
developers who want to create AST transforms. In fact, following transformers
are included so you can prototype your own plugins:

- [postcss][]

#### How to add a new parser

1. Go to `website/`.
2. Install the new parser as dependency: `yarn add theParser` (or `npm install -S theParser`)
3. Copy one of the existing examples in `src/parsers/{language}`.
4. Adjust the code as necessary:

- Update metadata.
- Load the right parser (`loadParser`).
- Call the right parsing method with the right/necessary options in `parse`.
- Implement the `nodeToRange` method (this is for highlighting).
- Implement the `getNodeName` method (this is for quick look through the tree).
- Implement `opensByDefault` method for auto-expansion of specific properties.
- Define `_ignoredProperties` set or implement `forEachProperty` generator method for filtering.
- Provide a `renderSettings` method if applicable.

#### How to add a new transformer

0. Go to `website/`.
1. Install the new transformer as dependency.
1. Copy one of the existing examples in `src/parsers/{language}/transformers`.
1. Adjust the code as necessary:

- Update metadata and `defaultParserID`.
- Load the right transformer (`loadTransformer`).
- Call the transformation method in `transform`.
- Change sample transformation code in `codeExample.txt`.

#### Build your own version for development

1. Clone the repository.
2. Go to `website/`.
3. Install all dependencies with `yarn install` (you can run `npm install` as
   well).

Run `yarn run build` for the final minimized version.
Run `yarn run watch` for incremental builds.

Run `yarn start` to start a simple static webserver.
