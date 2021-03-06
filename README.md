# eleventy-plugin-add-web-component-definitions

This plugin will automatically add Web Component definitions to your HTML pages

Given a page with this structure:
```html
<html>
  <body>
    <custom-tag></custom-tag>
  </body>
</html>
```

The plugin will transform it, with default options, into:
```html
<html>
  <body>
    <custom-tag></custom-tag>
    <script type="module" src="/js/components/custom-tag/custom-tag.js"></script>
  </body>
</html>
```

## How to use

First, install it:
```bash
npm install --save-dev eleventy-plugin-add-web-component-definitions
```

Then, in your `.eleventy.js` configuration file, add:
```js
// Together with your other imports
const addWebComponentDefinitions = require('eleventy-plugin-add-web-component-definitions')

module.exports = function(eleventyConfig) {

  // Inside your eleventy configuration function
  eleventyConfig.addPlugin(addWebComponentDefinitions)
}
```

### Options

| name           |  type      | default          | description         |
|----------------|------------|------------------|---------------------|
| `path`         | `Function` | ``function (tag) { return `/js/components/${tag}/${tag}.js\` `` | Path where your components are published |
| `position`     | `String`   | `beforeend`      | Position where the script tag will be put in regards to the `body` element, see other options in [MDN web](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML) |
| `verbose`      | `Boolean`  | `false`          | It will console log each step, for debug purposes |
| `quiet`        | `Boolean`  | `false`          | It won't console log anything. By default, a log of each Web Component definition is log out with this format: `[add-web-component-definitions] Adding definition for tag: custom-tag`|

### Example

Say your components live in `/components/` with no subfolders for tags and that your published website lives in a sub-folder of the domain (such as what happens in Github Pages or Gitlab Pages), you can do this:

```js
eleventyConfig.addPlugin(addWebComponentDefinitions, {
  path: tag => project.environment === 'production'
      ? `/my-project/components/${tag}.js`
      : `/components/${tag}.js`
  }
)
```

For a verbose output, do this:
```js
eleventyConfig.addPlugin(addWebComponentDefinitions, { verbose: true })
```

### Questions? Feature requests?

Please [open an issue](https://github.com/jdvivar/eleventy-plugin-add-web-component-definitions/issues/new) and I'll get back to you ASAP!