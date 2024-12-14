# greenspark-widget

A front-end service that allows a user to display product widgets as well as update their settings.

You can view the site hosted [here](https://sangshrestha.github.io/greenspark-widget/).

## Installation

```
npm i
```

```
npm run dev
```

## Data

Widget properties are fetched from the following endpoint:

```
https://b795b019-1f84-41f4-93a3-a702d686c75a.mock.pstmn.io/product-widgets
```

There's `dummy.ts` which serves similar data in case of error in detching.

## Input

`<input type="radio">` used in badge colour picker as well as activate badge selection to allow for only one active item at a time.
