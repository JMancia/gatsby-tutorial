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
