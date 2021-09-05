*This repository is a demonstration of how the Create Figma Plugin toolkit can be used to build a [FigJam Widget](https://www.figma.com/blog/bringing-the-power-of-our-open-platform-to-figjam/).*

First:

```
$ git clone https://github.com/yuanqing/widget
$ cd widget
$ npm install
```

`plugin-typings` is the folder containing the new `index.d.ts` typings file that’s provided in the Beta. Copy this folder into `widget/node_modules/@figma`:

```
$ cd ..
$ ls
widget  plugin-typings
$ rm -rf widget/node_modules/@figma/plugin-typings
$ cp -R plugin-typings widget/node_modules/@figma/plugin-typings
```

We’re now ready to run the `watch` script:

```
$ cd widget
$ npm run watch
```

---

For now, to launch a UI, use the `showUI` function from `src/show-ui.ts` instead of the `showUI` function from `@create-figma-plugin/utilities`.

The diff between `src/show-ui.ts` and the `showUI` from `@create-figma-plugin/utilities` is actually just a single line:

```diff
  /**
   * Renders the UI correponding to the command in a modal within the Figma UI.
   * Specify the modal’s `width`, `height`, `title`, and whether it is `visible`
   * via [`options`](https://figma.com/plugin-docs/api/properties/figma-showui/).
   * Optionally pass on some initialising `data` from the command to the UI.
   *
   * See how to [add a UI to a plugin command](#ui-1).
   *
   * @category UI
   */
  export function showUI<Data extends Record<string, unknown>>(
    options: ShowUIOptions,
    data?: Data
  ): void {
    if (typeof __html__ === 'undefined') {
      throw new Error('No UI defined')
    }
    const html = `<div id="create-figma-plugin"></div><script>const __FIGMA_COMMAND__='${
-     figma.command
+     ''
    }';const __SHOW_UI_DATA__=${JSON.stringify(
      typeof data === 'undefined' ? {} : data
    )};${__html__}</script>`
    figma.showUI(html, options)
  }
```

Create Figma Plugin will be updated accordingly when the FigJam Widget API stabilizes.
