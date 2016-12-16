# MDC Checkbox

The MDC Checkbox component is a spec-aligned checkbox component adhering to the
[Material Design checkbox requirements](https://material.google.com/components/selection-controls.html#selection-controls-checkbox).
It works without JavaScript with basic functionality for all states. If you use the JavaScript object for a checkbox, it will add more intricate animation effects when switching between states.

## Installation

```
npm install --save @material/checkbox
```

## Usage

### Standalone Checkbox

```html
<div class="mdc-checkbox">
  <input type="checkbox"
         class="mdc-checkbox__native-control"/>
  <div class="mdc-checkbox__background">
    <svg version="1.1" class="mdc-checkbox__checkmark"
         xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
         xml:space="preserve">
      <path class="mdc-checkbox__checkmark__path" fill="none" stroke="white"
            d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
    </svg>
  <div class="mdc-checkbox__mixedmark"></div>
</div>
```

The checkbox component is driven by an underlying native checkbox element. This element is sized and
positioned the same way as the checkbox component itself, allowing for proper behavior of assistive
devices.

You can also add an `mdc-checkbox--theme-dark` modifier class to the component to use the dark theme
checkbox styles.

Additionally, the checkbox can be used in conjunction with [mdc-form-field](../mdc-form-field) to
easily position checkboxes and their labels.

```html
<div class="mdc-form-field">
  <div class="mdc-checkbox">
    <input type="checkbox"
           class="mdc-checkbox__native-control"
           id="my-checkbox"/>
    <div class="mdc-checkbox__background">
      <svg version="1.1" class="mdc-checkbox__checkmark"
           xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"
           xml:space="preserve">
        <path class="mdc-checkbox__checkmark__path" fill="none" stroke="white"
              d="M1.73,12.91 8.1,19.28 22.79,4.59"/>
      </svg>
    <div class="mdc-checkbox__mixedmark"></div>
  </div>

  <label for="my-checkbox">My Checkbox Label</label>
</div>
```

### Using the JS Component

MDC Checkbox ships with a Component / Foundation combo which progressively enhances the checkbox
state transitions to achieve full parity with the material design motion for switching checkbox
states.

#### Including in code

##### ES2015

```javascript
import {MDCCheckbox, MDCCheckboxFoundation} from 'mdc-checkbox';
```

##### CommonJS

```javascript
const mdcCheckbox = require('mdc-checkbox');
const MDCCheckbox = mdcCheckbox.MDCCheckbox;
const MDCCheckboxFoundation = mdcCheckbox.MDCCheckboxFoundation;
```

##### AMD

```javascript
require(['path/to/mdc-checkbox'], mdcCheckbox => {
  const MDCCheckbox = mdcCheckbox.MDCCheckbox;
  const MDCCheckboxFoundation = mdcCheckbox.MDCCheckboxFoundation;
});
```

##### Global

```javascript
const MDCCheckbox = mdc.checkbox.MDCCheckbox;
const MDCCheckboxFoundation = mdc.checkbox.MDCCheckboxFoundation;
```

#### Automatic Instantiation

If you do not care about retaining the component instance for the checkbox, simply call `attachTo()`
and pass it a DOM element.  

```javascript
mdc.checkbox.MDCCheckbox.attachTo(document.querySelector('.mdc-checkbox'));
```

#### Manual Instantiation

Checkboxes can easily be initialized using their default constructors as well, similar to `attachTo`.

```javascript
import {MDCCheckbox} from 'mdc-checkbox';

const checkbox = new MDCCheckbox(document.querySelector('.mdc-checkbox'));
```

#### MDCCheckbox API

The MDCCheckbox API provides accessor properties similar to those found on a native checkbox element.

##### MDCCheckbox.checked

Boolean. Returns whether or not the checkbox is checked. Setting this property will update the
underlying checkbox element.

##### MDCCheckbox.indeterminate

Boolean. Returns whether or not the checkbox is indeterminate. Setting this property will update the
underlying checkbox element.

##### MDCCheckbox.disabled

Boolean. Returns whether or not the checkbox is disabled. Setting this property will update the
underlying checkbox element.

### Using the Foundation Class

MDC Checkbox ships with an `MDCCheckboxFoundation` class that external frameworks and libraries can
use to integrate the component. As with all foundation classes, an adapter object must be provided.
The adapter for checkboxes must provide the following functions, with correct signatures:

| Method Signature | Description |
| --- | --- |
| `addClass(className: string) => void` | Adds a class to the root element. |
| `removeClass(className: string) => void` | Removes a class from the root element. |
| `registerAnimationEndHandler(handler: EventListener) => void` | Registers an event handler to be called when an `animationend` event is triggered on the root element. Note that you must account for
vendor prefixes in order for this to work correctly. |
| `deregisterAnimationEndHandler(handler: EventListener) => void` | Deregisters an event handler from an `animationend` event listener. This will only be called with handlers that have previously been passed to `registerAnimationEndHandler` calls. |
| `registerChangeHandler(handler: EventListener) => void` | Registers an event handler to be called when a `change` event is triggered on the native control (_not_ the root element). |
| `deregisterChangeHandler(handler: EventListener) => void` | Deregisters an event handler that was previously passed to `registerChangeHandler`. |
| `getNativeControl() => HTMLInputElement?` | Returns the native checkbox control, if available. Note that if this control is not available, the methods that rely on it will exit gracefully.|
| `forceLayout() => void` | Force-trigger a layout on the root element. This is needed to restart
animations correctly. If you find that you do not need to do this, you can simply make it a no-op. |
| `isAttachedToDOM() => boolean` | Returns true if the component is currently attached to the DOM, false otherwise.` |

#### MDCCheckboxFoundation API

##### MDCCheckboxFoundation.isChecked() => boolean

Returns whether or not the underlying input is checked. Returns false when no input is available.

##### MDCCheckboxFoundation.setChecked(checked: boolean)

Updates the `checked` property on the underlying input. Does nothing when the underlying input is
not present.

##### MDCCheckboxFoundation.isIndeterminate() => boolean

Returns whether or not the underlying input is indeterminate. Returns false when no input is
available.

##### MDCCheckboxFoundation.setIndeterminate(indeterminate: boolean)

Updates the `indeterminate` property on the underlying input. Does nothing when the underlying input
is not present.

##### MDCCheckboxFoundation.isDisabled() => boolean

Returns whether or not the underlying input is disabled. Returns false when no input is available.

##### MDCCheckboxFoundation.setDisabled(disabled: boolean)

Updates the `disabled` property on the underlying input. Does nothing when the underlying input is
not present.

## Theming

> TK once mdc-theming lands.