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

## Part 3
The `gatsby-config.js` file is where plugins and other site configurations are added.
In this case, after installing Typography.js it can be added to the `gatsby-config.js` file.
```javascript
// gatsby-config.js

module.exports = {
  plugins: [
    {
      resolve: `gatsby-plugin-typography`,
      options: {
        pathToConfigModule: `src/utils/typography`,
      },
    },
  ],
}
```
A `typography.js` file is required inside the `src/utils/` directory.
Inside the `typography.js` file the themes that were installed can be imported and be automatically applied to the page.
```javascript
// src/utils/typography.js

import Typography from 'typography'
import fairyGateTheme from 'typography-theme-fairy-gates'

const typography = new Typography(fairyGateTheme)

export const { scale, rhythm, options } = typography
export default typography
```
Layout components can be created and added to pages to apply consistent layout styles to the site.
```jsx
// src/components/layout.js

import React from 'react'

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <h3>MySweetSite</h3>
    {children}
  </div>
)
```
The call to `{children}` will be the content that is placed within the `<Layout>...</Layout>` component tag.
```jsx
// src/pages/index.js

import React from 'react'
import Layout from '../components/layout'

export default () => (
  <Layout>
    <h1>Hi! I'm building a fake Gatsby site as part of a tutorial!</h1>
    <p>
      What do I like to do? Lots of course but definitely enjoy building
      websites.
    </p>
  </Layout>
)
```

Page navigation to other pages can also be added to the layout component.
```jsx
// src/components/layout.js

import React from 'react'
import { Link } from 'gatsby'

const ListLink = props => (
  <li style={{ display: `inline-block`, marginRight: `1rem` }}>
    <Link to={props.to}>{props.children}</Link>
  </li>
)

export default ({ children }) => (
  <div style={{ margin: `3rem auto`, maxWidth: 650, padding: `0 1rem` }}>
    <header style={{ marginBottom: `1.5rem` }}>
      <Link to="/" style={{ textShadow: `none`, backgroundImage: `none` }}>
        <h3 style={{ display: `inline` }}>MySweetSite</h3>
      </Link>
      <ul style={{ listStyle: `none`, float: `right` }}>
        <ListLink to="/">Home</ListLink>
        <ListLink to="/about/">About</ListLink>
        <ListLink to="/contact/">Contact</ListLink>
      </ul>
    </header>
    {children}
  </div>
)
```
