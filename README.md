# Gatsby Tutorial

## Part 1

React components defined in `src/pages/*.js` will automatically become a page.
For example, `src/pages/about.js` will become a page with a url path of `http://webaddress/about/`

Sub-components can be used to break the UI into reusable pieces.
The index and about page both use the `<h1>` tag. A `Header` component can be created and become reusable with other components.

```jsx
// src/components/header.js

import React from 'react'

export default () => <h1>This is a header.</h1>
```

To use the `Header` component, import the component to the desired page.

```jsx
// src/pages/about.js

import React from 'react'
import Header from '../components/header'

export default () => (
  <div>
    <Header />
  </div>
)
```

Attributes or in the case of components, properties used in components are called props. When a component has a prop, it can be passed to the defined component.
```jsx
// src/pages/about.js

export default () => (
  <div>
    <Header headerText="About Gatsby" />
  </div>
)
```
```jsx
// src/components/header.js

export default props => <h1>{props.headerText}</h1>
```

Gatsby has a `<Link />` component that can link to other pages that are created in `src/pages/` directory.
To use the `<Link />` component it needs to be imported to the page that is going to use it.
```jsx
// src/pages/index.js

import React from 'react'
import { Link } from 'gatsby'
import Header from '../components/header'

export default () => (
  <div>
    <Link to="/contact/">Contact</Link>
    <Header headerText="Hello Gatsby!" />
  </div>
)
```
When using the `<Link />` component to link between pages make sure the destination page already exists or else the link will go to the Gatsby 404 page.
Links to pages outside of the Gatsby project are to use the HTML `<a>` tag.

## Part 2
Global styles can be created with a `.css` file and can be imported to the `gatsby-browser.js` file to apply the style globally.
```javascript
// gatsby-browser.js

import './src/styles/global.css'
```
Using CSS Modules is another way of creating and writing `.css` files as `.module.css` files. CSS Modules can be imported in component files.
```css
// src/components/container.module.css

.container {
  margin: 3rem auto;
  max-width: 600px;
}
```
```jsx
// src/components/container.js

import React from 'react'
import containerStyles from './container.module.css'

export default ({ children }) => (
  <div className={containerStyles.container}>{children}</div>
)
```
The `containerStyles` in the className is the name given when the `.module.css` is imported. The `.container` after `containerStyles` is the CSS class in the `.css` file.
```
             import name   CSS class
className={containerStyles.container}
```
The `<Container />` component can be called in any page where the `.module.css` style can be applied.
```jsx
// src/pages/about-css-modules.js

import React from 'react'
import styles from './about-css-modules.module.css'
import Container from '../components/container'

export default () => (
  <Container>
    <h1>About CSS Modules</h1>
    <p>CSS Modules are cool</p>
  </Container>
)
```
