# vue-cli

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).

#### Transitions

* `transition` elements can be used to element a **SINGLE** element. Multiple elements, like lists, cannot be animated 
with this
* `enter` - is the initial state
* `enter-active` - is where the transition takes place
* `type` property tells Vue which property has control over the duration of the animation
* `appear` attribute runs the animation on the initial rendering of the component
* `enter-class, enter-active-class, leave-class, leave-active-class` allow you to override the `name` property in Vue and
create your own animations including libraries
* conditional elements rendered need a unique `key` so that Vue knows they're separate components
* `mode` - dictates order in which to animate components that are rendered conditionally. If `out-in` it will wait for the 
old element to animate out before animating the new one in. `In-out` will do the opposite.

#### Transition JS Hooks
* `before-enter` hook - 
* `enter` hook - 
* `after-enter` hook -
* `after-enter-cancelled` hook -  

#### Transition Groups
* for animating groups of elements (think lists)
* transition is not rendered in the dom
* transtion groups are rendered as a `span`, this can be overwritten w/ `transition-group tag="TAG"`
#### Animate CSS
* quick library for CSS
