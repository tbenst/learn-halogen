# Static HTML

We'll begin by first showing how to build a static HTML using Halogen's HTML DSL (domain specific language).

Starting small, there will not be any properties, css, or event handling. Rather, we'll just get used to the DSL itself. We'll render the following HTML that would appear in an HTML document's `body` element in Purescript
```html
<div>
    <div>
        <span>This is text in a span!</span>
    <div>
    <button>You can click me, but I don't do anything</button>
</div>
```

In PureScript, we would write this like so:
```purescript
import Halogen.HTML as HH
import Scaffolding.StaticRenderer (StaticHTML)

staticHtml :: StaticHTML
staticHtml =
  HH.div_
    -- The 'div' tag takes an Array of children
    [ HH.div_
      [ HH.span_
        -- as does the `span` tag
        [ HH.text "This is text in a span!" ]
      ]
    , HH.button_
      [ HH.text "You can click me, but I don't do anything." ]
    ]

```

## Where are the SVG elements?

By default, `purescript-halogen-vdom` includes most HTML elements. However, it does not include the SVG elements. To get that, we need to add [`purescript-halogen-svg`] as a dependency. Unfortunately, that library has not been updated to Halogen `v5.0.0`. It might also not compile on the current PureScript release.

Now, look at the next file.

## Compiling Instructions

To compile the next file and view its results in the browser, use these instructions.

```bash
spago bundle-app -m StaticHTML.StaticHTML -t assets/static-html/static-html.js
node node_modules/parcel/bin/cli.js serve assets/static-html/static-html.html -o static-html--parcelified.html --open
```

## Automatic Reload

To automatically reload the page upon saving the source `.purs` file, launch the `spago bundle-app` command in a separate terminal with the following [`watchexec`](https://github.com/watchexec/watchexec) prefix:
```
watchexec -w src -e purs --
```
The full command for this example is:
```
watchexec -w src -e purs -- spago bundle-app -m StaticHTML.StaticHTML -t assets/static-html/static-html.js
```
This prefix may be applied to all subsequent examples.
