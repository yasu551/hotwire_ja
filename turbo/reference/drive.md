---
permalink: /reference/drive.html
order: 01
description: "Turbo ドライブのリファレンス"
---

# Drive

## Turbo.visit

```js
Turbo.visit(location)
Turbo.visit(location, { action: action })
Turbo.visit(location, { frame: frame })
```

Performs an [Application Visit][] to the given _location_ (a string containing a URL or path) with the specified _action_ (a string, either `"advance"` or `"replace"`).
指定された _location_（URLまたはパスを含む文字列）に対して、指定された _action_（"advance" または "replace" のいずれかの文字列）でアプリケーション・アクセスを行います。

If _location_ is a cross-origin URL, or falls outside of the specified root (see [Setting a Root Location](/handbook/drive#setting-a-root-location)), Turbo performs a full page load by setting `window.location`.

If _action_ is unspecified, Turbo Drive assumes a value of `"advance"`.

Before performing the visit, Turbo Drive fires a `turbo:before-visit` event on `document`. Your application can listen for this event and cancel the visit with `event.preventDefault()` (see [Canceling Visits Before They Start](/handbook/drive#canceling-visits-before-they-start)).

If _frame_ is specified, find a `<turbo-frame>` element with an `[id]` attribute that matches the provided value, and navigate it to the provided _location_. If the `<turbo-frame>` cannot be found, perform a page-level [Application Visit][].

[Application Visit]: /handbook/drive#application-visits

## Turbo.cache.clear

```js
Turbo.cache.clear()
```

Removes all entries from the Turbo Drive page cache. Call this when state has changed on the server that may affect cached pages.

**Note:** This function was previously exposed as `Turbo.clearCache()`. The top-level function was deprecated in favor of the new `Turbo.cache.clear()` function.

## Turbo.setProgressBarDelay

```js
Turbo.setProgressBarDelay(delayInMilliseconds)
```

Sets the delay after which the [progress bar](/handbook/drive#displaying-progress) will appear during navigation, in milliseconds. The progress bar appears after 500ms by default.

Note that this method has no effect when used with the iOS or Android adapters.

## Turbo.setConfirmMethod

```js
Turbo.setConfirmMethod(confirmMethod)
```

Sets the method that is called by links decorated with [`data-turbo-confirm`](/handbook/drive#requiring-confirmation-for-a-visit). The default is the browser's built in `confirm`. The method should return `true` if the visit can proceed.

## Turbo.session.drive

```js
Turbo.session.drive = false
```

Turns Turbo Drive off by default. You must now opt-in to Turbo Drive on a per-link and per-form basis using `data-turbo="true"`.
