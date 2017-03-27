# cf-ui

> Cloudflare UI Framework

cf-ui is a set of over 50 packages used to build UIs at Cloudflare using
projects such as [React](https://facebook.github.io/react/),
[Fela](http://fela.js.org), [Lerna](https://lernajs.io) and more.

- **[Read the introductory blog post &rarr;](https://blog.cloudflare.com/cf-ui/)**
- **[Interested in more of our technical decisions? See `cf-ui/discussions` &rarr;](discussions)**

## cf-ui meets CSS in JS

We are currently migrating cf-ui to CSS in JS powered by [Fela](https://github.com/rofrischmann/fela). That means that our components include styles written in JavaScript and you can use them out of the box! However, you need to start using Fela in your project. [Follow our migration here](https://github.com/cloudflare/cf-ui/issues/100).

## Getting Started

To view all of the available components and packages, see the [`packages/` directory](packages). Do you want to see examples? Check out our [documentation](https://cloudflare.github.io/cf-ui/).

## CSS in JS setup

cf-ui components expect that there is [Fela Renderer](http://fela.js.org/docs/basics/Renderer.html) in the context of your React app. It's the way how to render styles that come with our components into the `<style></style>` node. **You have to use Fela in your project if you want to use cf-ui.** Here's the code example how:

```jsx
// React
import React from 'react';
import ReactDOM from 'react-dom';

// cf-ui component
import { Button as ButtonUnstyled, ButtonTheme } from 'cf-component-button';
import { applyTheme } from 'cf-style-container';

// Provider that enables Fela in your React project
import { createProvider } from 'cf-style-provider';

// cf-ui components export React components and themes, you have to combine
// them together first, we have our private set of wrapper components (cf-ux)
// that do just that, you might want to use your own theme
const Button = applyTheme(ButtonUnstyled, ButtonTheme);

// Empty DOM nodes for styles and React, note that everything can be server
// side rendered if you wish
const fontNode = document.getElementById('font-stylesheet');
const cssNode = document.getElementById('stylesheet');
const htmlNode = document.getElementById('react-app');

// Configure the style provider
const StyleProvider = createProvider({ cssNode, fontNode });

ReactDOM.render(
  <StyleProvider>
    <Button type="primary" onClick={() => console.log('clicked')}>
      Primary Button
    </Button>
  </StyleProvider>,
  htmlNode
);
```

Do you want to try for yourself?

```sh
git clone git@github.com:cloudflare/cf-ui.git
cd cf-ui/example
yarn install
yarn run build
open index.html
```

## Contributing

To get started contributing please see [CONTRIBUTING.md](CONTRIBUTING.md)

## License

cf-ui is [BSD Licensed](LICENSE)
