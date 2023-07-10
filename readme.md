Carrefour is an online groceries store, built using React, MobX, Stripe, and Universal Router.

Live demo: https://react-online-groceries-store.vercel.app/

![Screenshot from 2023-07-09 21-59-09](https://github.com/Vargriym/React-online-groceries-store/assets/102037554/179d4e69-1e43-4e89-9031-1761e55f5693)

## Mobx

<https://mobx.js.org/react-integration.html>

`yarn add mobx mobx-react-lite`

- configuration for debugging

```js
// #index.js
import { configure } from "mobx";
configure({
  enforceActions: "always",
  computedRequiresReaction: true,
  reactionRequiresObservable: true,
  observableRequiresReaction: true,
  disableErrorBoundaries: true,
});
```


## Universal Router

Based on an object of routes that will be parsed. Not integrated within React (different from React Router)

<https://github.com/kriasoft/universal-router/blob/master/docs/api.md>

- Build a `routes`, array of objects `{path:"/", action:()=>{..}}`.
- Use a listener on **history**
- Use `history.push` for ajax on each `<a>` click,
- For route resolving and rendering, `new UniversalRouter(routes).resolve` in **index.js**
- pass the `store` to the `routes` so every path/action has access to

Using the middleware `next` to pass `{children}` into a menu layout. This is done twice, for general menu, and for the general submenu (nested routes).

## Component **ProductDetails** with ".dot" notation


To be able to `import` two components, I made object with several components:

```js
const ProductDetails = {
  getDetail: fetch(...),
  Storage,
  Info,
  Nutrition,
  Details,
};
```

## Saving to localStorage

When the app is started with **index.js**, we read localStorage with the IFFE `action(() => store.initCart())()`

The cart is saved to loalStorage in the **Product** component within a `useEffect` with `runInAction`.
