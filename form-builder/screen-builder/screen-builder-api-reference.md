---
description: >-
  This reference guide documents functions and methods for ProcessMaker's Screen
  Builder.
---

# Screen Builder API Reference

## Overview

This reference guide documents the functions (or events), and methods offered in ProcessMaker's [Screen Builder](https://github.com/ProcessMaker/screen-builder). This reference provides in-depth explanations, code examples, and best practices to assist you in fully utilizing the capabilities of Screen Builder.

{% hint style="info" %}
`@processmaker/screen-builder` is a VueJS powered Screen Builder that produces compatible JSON for our vue-form-renderer.
{% endhint %}

## Global Event Bus

The `window.ProcessMaker.EventBus` object serves as an independent Vue instance that acts as the application's global event bus. This object provides a centralized mechanism for communication and event handling within ProcessMaker's Screen Builder.

Screen Builder emits essential events on the event bus in which to monitor from application code to hook into, customize, and extend the behavior of Screen Builder.

### `screen-renderer-build-component` Event

The `screen-renderer-build-component` event plays a crucial role in the building process of components. When this event is emitted, it triggers the necessary actions and logic to build the components effectively. By handling the `screen-renderer-build-component` event, the application ensures that the components are built accurately.

#### Signature

```javascript
window.ProcessMaker.EventBus.$emit(event, payload);
```

#### Parameters

* `event`: The name of the event to emit. It should be a string value.
* `payload` (optional): Any additional data or payload to pass along with the event. It can be of any type.

#### Example

```javascript
window.ProcessMaker.EventBus.$emit('screen-renderer-build-component', this);
```

### `screen-renderer-init` Event

The `screen-renderer-init` event plays a vital role in initializing the components and setting their initial state. By emitting this event, the code effectively signals to other parts of the application that the component initialization process is underway.

#### Signature

```javascript
window.ProcessMaker.EventBus.$emit(event, payload);
```

#### Parameters

* `event`: The name of the event to emit. It should be a string value.
* `payload` (optional): Any additional data or payload to pass along with the event. It can be of any type.

#### Example

```javascript
window.ProcessMaker.EventBus.$emit('screen-renderer-init', this);
```

## Methods

This section describes the available methods in ProcessMaker's Screen Builder. To empower developers to leverage Screen Builder's potential and create highly customized and tailored solutions.

Before we dive into methods, let's understand the following modules and components that are essential for the functionality and customization of Screen Builder.&#x20;

* **lodash:** lodash is a powerful utility library that provides various helpful functions to manipulate and work with data in Screen Builder. It can be used for tasks such as data transformation, array manipulation, object manipulation, and more.
* **extensions:** The `extensions` module contains custom extensions or plugins specific to Screen Builder. These extensions can enhance the functionality of Screen Builder by providing additional features, components, or tools for building Screens.
* **ScreenBase:** ScreenBase is a foundational module that defines the base Screen component for Screen Builder. This base component serves as a starting point to create customized Screen components by extending its functionality and adding specific features or behavior.
* **CountElements:** CountElements contains utility functions or components related to counting elements within Screen Builder. These utilities can be used to calculate and track the number of elements present in a Screen or perform calculations based on the elements present.
* **ValidationsFactory:** ValidationsFactory provides a factory function or class specifically designed to manage validation rules within Screen Builder. It enables the creation, configuration, and management of validation rules for various form elements and data inputs in the Screens built using Screen Builder.

### Example to Import the Modules and Components

```javascript
import _ from "lodash";
import extensions from './extensions';
import ScreenBase from './ScreenBase';
import CountElements from '../CountElements';
import ValidationsFactory from '../ValidationsFactory';
```

### Method: `buildComponent`

This method builds a component based on the provided definition.

#### Signature

```javascript
buildComponent(definition: string): void
```

#### Parameters

* `definition`: The definition of the component to build.

#### Example

```javascript
buildComponent("<div>Example Component</div>");
```

### Method: `loadPages`

This method loads the pages defined in the given definition into the owner element.

#### Signature

```javascript
loadPages(definition: object, owner: HTMLElement, screen: string): void
```

#### Parameters

* `definition`: The definition object containing page configurations.
* `owner`: The element to which the pages will be loaded.
* `screen`: The Screen identifier.

#### Example

```javascript
loadPages(definitionObject, document.getElementById("pageContainer"), "screen1");
```

### Method: `updateComponentConfig`

This method updates the properties of a component configuration.

#### Signature

```javascript
updateComponentConfig(config: object, props: object): object
```

#### Parameters

* `config`: The original component configuration object.
* `props`: The updated properties object.

#### Example

```javascript
const updatedConfig = updateComponentConfig(originalConfig, { prop1: "new value" });
console.log(updatedConfig); // Output: { prop1: "new value", prop2: "value2" }
```

### Method: **`createComponent`**

This method creates a new component by dynamically generating an HTML element with the specified `nodeName` and applying the given `properties` to the element as attributes.

#### Signature

```javascript
createComponent(nodeName: string, properties: object): HTMLElement
```

#### Parameters

* `nodeName` (string): The name of the HTML element to be created for the component.
* `properties` (object): An object containing key-value pairs representing the properties to be applied to the component. The keys represent the property names, and the values represent the property values.

#### Example

```javascript
// Create a component with the nodeName 'div' and properties
const component = createComponent('div', {
  class: 'my-component',
  id: 'component-1',
  style: 'color: blue;',
});

console.log(component);
```

### Method: **`loadItems`**

This method iterates over an array of `items` and dynamically loads them into a specified `component`. Each item in the array represents a configuration element, and the method creates corresponding components based on the element's properties.

#### Signature

```javascript
loadItems(items: Array<object>, component: HTMLElement, screen: string, definition: object, formIndex: number): void
```

#### Parameters

* `items` (Array\<object>): An array of configuration items, where each item represents a configuration element.
* `component` (HTMLElement): The component or container element where the dynamically created components will be appended.
* `screen` (string): The Screen or context in which the components are being loaded.
* `definition` (object): The definition or configuration object for the components.
* `formIndex` (number): The index of the form or section where the components are being loaded.

#### Example

```javascript
// Define an array of items
const items = [
  {
    nodeNameProperty: 'nodeName',
    config: { class: 'item', id: 'item-1' },
  },
  {
    nodeNameProperty: 'nodeName',
    config: { class: 'item', id: 'item-2' },
  },
];

// Create a component and load the items into it
const component = document.getElementById('my-component');
loadItems(items, component, 'main-screen', { ... }, 0);
```

### Method: **`setDefaultPropertyValues`**

This method sets default values for certain properties in the `props` object. It checks if specific properties are undefined, null, or empty strings and assigns default values to them.

#### Signature

```javascript
setDefaultPropertyValues(props: object): object
```

#### Parameters

* `props` (object): An object containing the properties for which default values need to be set.

#### Example

```javascript
// Define an object with properties
const properties = {
  ariaLabel: null,
  label: 'Example Label',
  tabindex: '3',
};

// Set default property values
const defaultValues = setDefaultPropertyValues(properties);
console.log(defaultValues);
```

### Method: **`addValidationRulesLoader`**

This method adds a validation rules loader to a component. It is responsible to asynchronously load validation rules and update the component's `ValidationRules__` property.

#### Signature

```javascript
addValidationRulesLoader(component: object, definition: object)
```

#### Parameters

* `component` (object): The component to which the validation rules loader will be added.
* `definition` (object): The definition object containing information about the Screen and data.

#### Example

```javascript
// Define a component and a definition object
const component = {
  methods: {},
  mounted: [],
};
const definition = {
  // ...definition properties
};

// Add validation rules loader to the component
addValidationRulesLoader(component, definition);
console.log(component);
```

### Method: **`mounted`**

{% hint style="info" %}
Document Object Model (DOM) represents the structure of a web page as a hierarchical tree of objects, where each object represents a part of the document, such as an element, attribute, or text node.
{% endhint %}

This method is executed when the component is mounted to the DOM. It checks if the `screenRenderer` instance exists and creates a new instance if it does not. The `screenRenderer` instance is created using the constructor of the current component and is mounted to the DOM.

#### Signature

```javascript
mounted()
```

#### Example

```javascript
// Define a component
const component = {
  mounted() {
    if (!screenRenderer) {
      screenRenderer = new this.constructor({
        propsData: {
          value: {},
          definition: {config: []},
        },
      });
      screenRenderer.$mount();
    }
  },
};

// Mount the component
component.mounted();
console.log(screenRenderer);
```

## Conclusion

In summary, developers can leverage this comprehensive reference guide to enhance their proficiency in utilizing the ProcessMaker's Screen Builder effectively. Therefore, by understanding the functions, events, and methods, developers can unlock the full potential of the Screen Builder and customize it to their business needs.
