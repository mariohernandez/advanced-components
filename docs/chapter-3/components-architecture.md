# Components architecture

Components are typically saved in a project's theme and although they will work regardless of where in your theme they are stored, it is recommended to group them in folders. This not only provides organization as your catalog of components grows, but it also makes each component completely reusable and even portable as all the pieces of a component are encapsulated in a single folder. Here's a typical architecture of a component. Your particular workflow may vary.

```text
+-- ..
|
|-- _patterns/
|   |-- 01-patterns/
|       |-- card/
|         |-- card.es6.js
|         |-- card.md
|         |-- card.twig
|         |-- card.scss
|         |-- card.yml
|
+-- ..
```

A component is typically broken down in four parts:

**Markup**: Markup for a component is written using Twig, Drupal's new templating engine. Naming convention for a component twig template looks like this: card.twig \(where card is the name of the component\).

**Data**: For the purpose of the style-guide, we need dummy or stock data, which is normally provided in YAML or JSON format. In this workshop we will use YAML.

**Styles**: These are written in CSS or SCSS.

**Behavior/interaction**: The component's behaviors are usually handled with JavaScript. Our theme supports ES6 and through a gulp task we convert it to plain JS.

**Annotations \(Optional\)**: Annotations are used to document the details of a component and are typically written in markdown format. This is extremely useful for developers because it outlines technical details of a pattern such as variable names, attributes, data structure, etc.

> **NOTE**: Not every component will need a javascript file.

