---
version: v0.37.3
category: API
title: 'Power Save Blocker'
source_url: 'https://github.com/atom/electron/blob/master/docs/api/power-save-blocker.md'
---

# powerSaveBlocker

The `powerSaveBlocker` module is used to block the system from entering
low-power (sleep) mode and thus allowing the app to keep the system and screen
active.

For example:

```javascript
const powerSaveBlocker = require('electron').powerSaveBlocker;

var id = powerSaveBlocker.start('prevent-display-sleep');
console.log(powerSaveBlocker.isStarted(id));

powerSaveBlocker.stop(id);
```

## Methods

The `powerSaveBlocker` module has the following methods:

### `powerSaveBlocker.start(type)`

* `type` String - Power save blocker type.
  * `prevent-app-suspension` - Prevent the application from being suspended.
    Keeps system active but allows screen to be turned off.  Example use cases:
    downloading a file or playing audio.
  * `prevent-display-sleep`- Prevent the display from going to sleep. Keeps
    system and screen active.  Example use case: playing video.

Starts preventing the system from entering lower-power mode. Returns an integer
identifying the power save blocker.

**Note:** `prevent-display-sleep` has higher has precedence over
`prevent-app-suspension`. Only the highest precedence type takes effect. In
other words, `prevent-display-sleep` always takes precedence over
`prevent-app-suspension`.

For example, an API calling A requests for `prevent-app-suspension`, and
another calling B requests for `prevent-display-sleep`. `prevent-display-sleep`
will be used until B stops its request. After that, `prevent-app-suspension`
is used.

### `powerSaveBlocker.stop(id)`

* `id` Integer - The power save blocker id returned by `powerSaveBlocker.start`.

Stops the specified power save blocker.

### `powerSaveBlocker.isStarted(id)`

* `id` Integer - The power save blocker id returned by `powerSaveBlocker.start`.

Returns a boolean whether the corresponding `powerSaveBlocker` has started.
