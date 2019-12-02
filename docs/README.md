# Introduction

## What is Yew?

**Yew** is a [Rust](https://www.rust-lang.org/) framework for creating multi-threaded front-end web apps with [WebAssembly](https://webassembly.org/).

#### Why Rust?

Rust is blazing fast and reliable with its rich type system and ownership model. It can have a tough learning curve but is well worth the effort. Rust has been voted the most loved programming language multiple years in a row in [Stack Overflow](https://insights.stackoverflow.com/survey/2018#technology-_-most-loved-dreaded-and-wanted-languages) [Developer Surveys](https://insights.stackoverflow.com/survey/2019#technology-_-most-loved-dreaded-and-wanted-languages). 

**Why WebAssembly?**

WebAssembly _\(Wasm\)_ is a portable low-level language that Rust can compile into which aims to run at native speeds in the browser and is interoperable with JavaScript and supported in all major browsers. 

### Modern Web Framework

Yew is a component-based framework that makes it easy to create interactive UIs. Developers who have experience with frameworks like React and Elm should feel quite at home when using Yew. Creating HTML in Yew even looks a lot like React's JSX with a few minor exceptions. Here's a quick look:

```rust
fn view(&self) -> Html<Self> {
  html! {
    <section class="todoapp">
      <header class="header">
        <h1>{ "todos" }</h1>
      </header>
      <section class="main">
        <input type="checkbox"
            checked=self.all_completed()
            onclick=|_| Msg::ToggleAll />
        { self.view_todos() }
      </section>
    </section>
  }
}
```

### Performance and Concurrency

Yew makes it easy to build performant applications by minimizing the number of expensive DOM API calls and making it simple to offload processing to background workers. For more ideas on how to get the most out of WebAssembly, check out this list of [Use Cases](https://webassembly.org/docs/use-cases/).

However, it should be noted that using Wasm is not a silver bullet for improving the performance of a web app. As of right now, using DOM APIs from WebAssembly is still slower than calling them directly from JavaScript. This is a temporary hurdle which the [WebAssembly Interface Types](https://github.com/WebAssembly/interface-types/blob/master/proposals/interface-types/Explainer.md) proposal aims to resolve. If you would like to learn more, check out this [excellent article](https://hacks.mozilla.org/2019/08/webassembly-interface-types/) from Mozilla.

### Type Safety and Reliability 

Rust helps developers write safer code with its rich type system and ownership model. Say goodbye to hard to track down race condition bugs in JavaScript! In fact, with Rust, most of your bugs will be caught by the compiler before your app even runs, often with a very helpful error message explaining what went wrong. Rust also encourages proper error handling and in the uncommon case that your app panics, you can even get full stack-traces for your Rust code in the browser console.

### JavaScript Interop

Yew is built on top of great web tooling created by the Rust community. It's easy to call JavaScript code from Rust and vice-versa, enabling you to try out Yew for a small part of your web app without any headaches. It's even possible to use your favorite NPM packages within Yew! 

### 
