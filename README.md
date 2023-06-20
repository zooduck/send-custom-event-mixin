# sendCustomEventMixin

A mixin for making non-element classes eventful.

## For users with an access token

Add a `.npmrc` file to your project, with the following lines:

```text
@zooduck:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=YOUR_ACCESS_TOKEN
```

Install from the command line:

```node
npm install @zooduck/send-custom-event-mixin@latest
```

Install via package.json:

```json
"@zooduck/send-custom-event-mixin": "latest"
```

## For users without an access token

Clone or [Download](https://github.com/zooduck/send-custom-event-mixin/archive/refs/heads/master.zip) the repository to your machine.

## Import

```javascript
import { sendCustomEventMixin } from 'path/to/send-custom-event-mixin/dist/index.module.js'
```

## Examples

Add an event listener using an event handler property:

```javascript
class Eventful extends sendCustomEventMixin() {
  constructor() {
    super()
  }
}
const eventful = new Eventful()
eventful.onmycustomevent = (event) => console.log(event.type, event.detail)
eventful.sendCustomEvent('mycustomevent', { detail: 'abc' })

// Logs: mycustomevent abc
```

Add an event listener using `addEventListener()`:

```javascript
eventful.addEventListener('mycustomevent', (event) => {
  console.log(event.type)
})
eventful.sendCustomEvent('mycustomevent')

// Logs: mycustomevent
```

Dispatch an event on both the class instance and the window:

```javascript
window.addEventListener('mycustomevent', (event) => {
  console.log(event.type)
})
eventful.sendCustomEvent('mycustomevent', { dispatchEventOnWindow: true })

// Logs: mycustomevent
```
