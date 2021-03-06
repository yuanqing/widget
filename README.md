# widget

> A demonstration of how the [Create Figma Plugin](https://yuanqing.github.io/create-figma-plugin/) toolkit can be used to build a [FigJam Widget](https://figma.com/blog/bringing-the-power-of-our-open-platform-to-figjam/)

## Initial set up

First:

```
$ git clone https://github.com/yuanqing/widget
$ cd widget
$ npm install
```

Suppose that `plugin-typings` is the folder containing the new `index.d.ts` typings file that’s provided in the FigJam Widgets Beta. Copy that folder into `widget/node_modules/@figma`:

```
$ cd ..
$ ls
widget  plugin-typings
$ rm -rf widget/node_modules/@figma/plugin-typings
$ cp -R plugin-typings widget/node_modules/@figma/plugin-typings
```

## Build the widget

We’re now ready to run the `watch` script:

```
$ cd widget
$ npm run watch
```

## Implementation details

- The `/** @jsx figma.widget.h */` [JSX pragma](https://typescriptlang.org/tsconfig#jsxFactory) is added to the top of the [`src/main.tsx`](/src/main.tsx) file.
  - This is necessary to allow esbuild (which powers the `build-figma-plugin` CLI) to correctly transpile the JSX used for defining the Widget into corresponding JavaScript function calls.

- A [`build-figma-plugin.manifest.js`](/build-figma-plugin.manifest.js) file is used to add a `"containsWidget"` key to the generated `manifest.json` file.
  - The `build-figma-plugin.manifest.js` file is an escape hatch for modifying the `manifest.json` just before it gets output by the `build-figma-plugin` CLI. This should no longer be necessary when `"containsWidget"` is added as an official [configuration option](https://yuanqing.github.io/create-figma-plugin/#configuration-options) when the FigJam Widgets API is stable.
