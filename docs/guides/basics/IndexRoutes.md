# Index Routes and Index Links

## Index Routes

To illustrate the use case for `IndexRoute`, imagine the following route
config without it:

```js
<Router>
  <Route path="/" component={App}>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>
```

When the user visits `/`, the App component is rendered, but none of the
children are, so `this.props.children` inside of `App` will be undefined.
To render some default UI you could easily do `{this.props.children ||
<Home/>}`.

But now `Home` can't participate in routing, like the `onEnter` hooks,
etc. You render in the same position as `Accounts` and `Statements`, so
the router allows you have `Home` be a first class route component with
`IndexRoute`.

```js
<Router>
  <Route path="/" component={App}>
    <IndexRoute component={Home}/>
    <Route path="accounts" component={Accounts}/>
    <Route path="statements" component={Statements}/>
  </Route>
</Router>
```

Now `App` can render `{this.props.children}` and we have a first-class
route for `Home` that can participate in routing.

## Index Links

If you were to `<Link to="/">Home</Link>` in this app, it would always
be active since every URL starts with `/`. This is a problem because
we'd like to link to `Home` but only be active if `Home` is rendered.

To have a link to `/` that is only active when the `Home` route is
rendered, use `<IndexLink to="/">Home</IndexLink>`.
