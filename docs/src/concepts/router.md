---
description: Yew's official router
---

# Router

[https://crates.io/yew-router](https://crates.io/yew-router)

Routers in Single Page Applications \(SPA\) handle displaying different pages depending on what the URL is. Instead of the default behavior of requesting a different remote resource when a link is clicked, the router instead sets the URL locally to point to a valid route in your application. The router then detects this change and then decides what to render.

## Core Elements

### Route

Contains a String representing everything after the domain in the url and optionally the state stored in the history api.

### RouteService

Communicates with the browser to get and set Routes.

### RouteAgent

Owns a RouteService and is used to coordinate updates when the route changes, either from within the application logic or from an event fired from the browser.

### Switch

The `Switch` trait is used to convert a `Route` to and from the implementer of this trait.

### Router

The Router component communicates with `RouteAgent` and will automatically resolve Routes it gets from the agent into switches, which it will expose via a `render` prop that allows specifying how the resulting switch gets converted to `Html`.

## How to use the Router

First, you want to create a type that represents all the states of your application. Do note that while this typically is an enum, structs are supported as well, and that you can nest other items that implement `Switch` inside.

Then you should derive `Switch` for your type. For enums, every variant must be annotated with `#[to = "/some/route"]`, or if you use a struct instead, that must appear outside the struct declaration.

Do note that the implementation generated by the derive macro for `Switch` will try to create each variant in order from first to last, so if any route could possibly match two of your specified `to` annotations, then the first one will match, and the second will never be tried.

You can also capture sections using variations of `{}` within your `#[to = ""]` annotation. `{}` means capture text until the next separator \(either "/", "?", "&", or "\#" depending on the context\). `{*}` means capture text until the following characters match, or if no characters are present, it will match anything. `{<number>}` means capture text until the specified number of separators are encountered \(example: `{2}` will capture until two separators are encountered\).

For structs and enums with named fields, you must specify the field's name within the capture group like so: `{user_name}` or `{*:age}`.

The Switch trait works with capture groups that are more structured than just Strings. You can specify any type that implements `Switch`. So you can specify that the capture group is a `usize`, and if the captured section of the URL can't be converted to it, then the variant won't match.  

