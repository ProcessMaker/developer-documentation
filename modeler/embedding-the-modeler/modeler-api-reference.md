---
description: >-
  This reference guide comprehensively covers the functions, events, and objects
  offered by the ProcessMaker Modeler.
---

# Modeler API Reference

## Overview

This comprehensive guide provides an in-depth exploration of the ProcessMaker Modeler, which empowers developers to interact with and customize the functionalities of the Modeler.

{% hint style="info" %}
The `@processmaker/modeler` is a powerful BPMN modeler built on Vue.js and scaffolded using [Vue CLI 3](https://cli.vuejs.org/). This modern and flexible framework provides developers with a solid foundation for creating dynamic and interactive BPMN modeling applications.
{% endhint %}

This reference guide comprehensively covers the functions, events, and objects offered by the ProcessMaker Modeler. It provides in-depth explanations, code examples, and best practices to assist you in fully utilizing the capabilities of the Modeler.

## Global Event Bus

The `window.ProcessMaker.EventBus` object serves as an independent Vue instance that acts as the application's global event bus. It provides a centralized mechanism for communication and event handling within the ProcessMaker Modeler.

The Modeler emits essential events on the event bus, which developers can listen to in their application code to hook into, customize, and extend the behavior of the Modeler:

### `modeler-init` Event

The `modeler-init` event is fired before the modeler is set up and mounted and is emitted by the `window.ProcessMaker.EventBus` object.&#x20;

#### Signature

```javascript
window.ProcessMaker.EventBus.$on('modeler-init', ({ registerBpmnExtension, registerNode, registerInspectorExtension }) => {
  // Initialization tasks and configuration code here
});
```

#### Parameters

The callback function for the `modeler-init` event receives an object with the following parameters:

* `registerBpmnExtension` (function): A function that registers a BPMN extension with the Modeler. Developers can use this function to add custom BPMN elements, properties, or attributes to the Modeler.
* `registerNode` (function): A function that registers a component to be used as a node in the Modeler. Developers can define custom nodes and register them using this function.
* `registerInspectorExtension` (function): A function that registers custom properties or extensions for the inspector panel. Developers can use this function to add additional properties or configuration options for specific Modeler elements.

#### Example

```javascript
import bpmnExtension from '@processmaker/processmaker-bpmn-moddle/resources/processmaker.json';
import { intermediateMessageCatchEvent } from '@/components/nodes';

window.ProcessMaker.EventBus.$on('modeler-init', ({ registerBpmnExtension, registerNode, registerInspectorExtension }) => {
  // Add a BPMN extension
  registerBpmnExtension('pm', bpmnExtension);

  // Register a component to be used in the modeler
  registerNode(intermediateMessageCatchEvent);

  // Add custom properties to the inspector
  registerInspectorExtension(intermediateMessageCatchEvent, {
    id: 'pm-condition',
    component: 'FormInput',
    config: {
      label: 'Condition',
      helper: 'Expression to be evaluated on webhook to activate event. Leave blank to accept always.',
      name: 'pm:condition',
    },
  });
});
```

### **`modeler-start` Event**

The `modeler-start` event is fired by the `window.ProcessMaker.EventBus` object after the ProcessMaker Modeler has been set up and mounted. This event provides an opportunity for developers to perform additional tasks or customizations that need to be executed after the Modeler has started.

#### Signature

```javascript
window.ProcessMaker.EventBus.$on('modeler-start', ({ loadXML }) => {
  // Additional tasks after the Modeler has started
});
```

#### Parameters

The callback function for the `modeler-start` event receives an object with the following parameter:

* `loadXML` (function): A method that allows developers to load an XML document into the Modeler. This method takes a string representation of the XML document as its argument.

#### Example

```javascript
window.ProcessMaker.EventBus.$on('modeler-start', ({ loadXML }) => {

  // Example: Load XML document into the Modeler
  loadXML('<?xml version="1.0" encoding="UTF-8"?> ... </bpmn:definitions>');
});
```

### `modeler-change` Event

The `modeler-change` event is fired by the `window.ProcessMaker.EventBus` object whenever a change is made to the ProcessMaker Modeler that results in a modification of the underlying XML representation. This event is triggered immediately after the new state is pushed to the undo/redo stack.

By listening to the `modeler-change` event, developers can perform actions or execute code in response to these modifications. This can include updating UI elements, saving the modified XML, triggering additional functionality, or any other desired behavior.

#### Signature

```javascript
window.ProcessMaker.EventBus.$on('modeler-change', () => {
  // Code to handle the change event
});
```

#### Parameters

The callback function for the modeler-change event does not receive any parameters.

#### Example

```javascript
window.ProcessMaker.EventBus.$on('modeler-change', () => {
  // Perform actions or execute code in response to diagram changes
  console.log('The diagram has changed');
  
  // Example: Update UI elements
  updateUI();

  // Example: Save the modified Diagram
  saveBpmn();
});
```

### `modeler-validate` Event

The `modeler-validate` event on the global event bus allows adding custom validation rules during the linting process. This allows developers to perform custom validation logic and report errors if needed.

{% hint style="info" %}
By default, the ProcessMaker modeler automatically validates the diagram as you create it. This validation can be toggled on and off using the switch in the status bar. Validation is handled using [bpmnlint](https://github.com/bpmn-io/bpmnlint)
{% endhint %}

#### Signature

```javascript
window.ProcessMaker.EventBus.$on('modeler-validate', (node, reporter) => {
  // Validation code goes here
});
```

#### Parameters

* `node` (object): The node to be validated.
* `reporter` (object): The reporter object to raise errors.

#### Example

```javascript
window.ProcessMaker.EventBus.$on('modeler-validate', (node, reporter) => {
  if (typeof node.id === 'string' && !node.id.startsWith('node_')) {
    reporter.report(node.id, 'Node ID must start with the string "node_"');
  }
});
```

In the example above, the event handler checks if the `node` has a valid ID, and if not, it reports an error using the `reporter.report` method.

By implementing custom validation logic within the `modeler-validate` event, developers can enforce specific rules or constraints on the elements in your modeler and provide meaningful error messages when those rules are violated.

## Methods

This section of the reference guide provides a comprehensive overview of the available methods in the ProcessMaker Modeler. Each method is documented, offering an explanation of its purpose, signature, parameters, and a practical code example. By familiarizing themselves with these methods and harnessing their capabilities, developers can seamlessly interact with the Modeler's functionality and tailor it to meet their unique BPMN modeling requirements.

The following modules and components are essential for the functionality and customization of the ProcessMaker Modeler. These dependencies provide a rich set of features and extend the capabilities of the modeler.

* **Vue**: The Vue library serves as the foundation for building interactive user interfaces in the Modeler.
* **lodash**: Lodash is a powerful utility library that offers a wide range of functions for efficient data manipulation and processing.
* **jointjs**: The jointjs library provides advanced diagramming capabilities through its 'dia' module, enabling the creation and manipulation of BPMN diagrams.
* **boundaryEventConfig**: This component defines the configuration for boundary events, allowing developers to customize their behavior and appearance.
* **InspectorPanel**: The InspectorPanel component provides an interface for inspecting and modifying the properties of BPMN elements.
* **ToolBar**: The ToolBar component offers a set of tools and actions for interacting with the Modeler, such as creating, editing, and deleting BPMN elements.
* **BpmnModdle**: This module enables the parsing and manipulation of BPMN models, providing access to the underlying BPMN elements and their properties.
* **Linter**: The Linter module integrates a BPMN linter into the Modeler, allowing developers to enforce coding standards and best practices.
* **XMLManager**: The XMLManager module handles XML-related operations, such as loading and saving BPMN models in XML format.
* **Node**: The Node component represents a BPMN node in the Modeler, providing methods and properties for customization and interaction.
* **TimerEventNode**: This component extends the Node component and represents a timer event in BPMN models, allowing developers to define and manage time-based events.

### Method: `isAppleOS`

Checks if the user's operating system is Apple-based (Mac, iPad, or iPhone).

#### Signature

```javascript
isAppleOS();
```

#### Returns

`boolean` - Returns `true` if the operating system is Apple-based, `false` otherwise.

#### Example

```javascript
const isApple = isAppleOS();
console.log(isApple); // Output: true or false
```

### Method: `shapeResize`

Resizes the shape based on the updated selection.

#### Signature

```javascript
shapeResize(clearIfEmpty = true)
```

#### Parameters

* `clearIfEmpty` (optional): A boolean flag indicating whether to clear the selection if it is empty defaults to `true`.

#### Example

```javascript
await shapeResize();
```

### Method: `toggleDefaultFlow`

Toggles the default flow of a BPMN element.

#### Signature

```javascript
toggleDefaultFlow(flow)
```

#### Parameters

* `flow`: The flow object to be set as the default flow.

#### Example

```javascript
const flow = getFlowObject();
toggleDefaultFlow(flow);
```

### Method: `cloneElement`

Clones a given BPMN element.

#### Signature

```javascript
cloneElement(node, copyCount)
```

#### Parameters

* `node`: The node to be cloned.
* `copyCount`: The number of times the node has been copied.

#### Example

```javascript
const node = getNodeToClone();
const count = 2;
cloneElement(node, count);
```

### Method: `copyElement`

Copies selected BPMN elements.

#### Signature

```javascript
copyElement()
```

#### Example

```javascript
copyElement();
```

### Method: `pasteElements`

Pastes copied BPMN elements.

#### Signature

```javascript
pasteElements()
```

#### Example

```javascript
await pasteElements();
```

### **Method**: `getXmlFromDiagram`

Retrieves the XML representation of the BPMN diagram.

#### Signature

```javascript
getXmlFromDiagram()
```

#### Parameters

```javascript
const xml = await getXmlFromDiagram();
```

### **Method**: `registerBpmnExtension`

Register a BPMN Moddle extension to support extensions to the BPMN XML format.

#### Signature

```javascript
registerBpmnExtension(namespace, extension)
```

#### Parameters

* `namespace` (String): The namespace of the extension.
* `extension` (Object): The extension object to register.

#### Example

```javascript
registerBpmnExtension(namespace, extension);
```

### **Method**: `loadArtifacts`

Loads artifacts in the BPMN diagram.

#### Signature

```javascript
loadArtifacts(flowElements, artifacts)
```

#### Parameters

* `flowElements` (Array): The array of flow elements.
* `artifacts` (Array): The array of artifacts.

#### Example

```javascript
loadArtifacts(flowElements, artifacts);
```

### **Method**: `renderPaper`

Renders the paper by performing atomic actions, parsing the BPMN diagram, adding pools, and setting up the diagram.

#### Signature

```javascript
renderPaper()
```

#### Example

```javascript
await renderPaper();
```

### **Method**: loadXML

Loads the BPMN diagram from XML, renders the paper, and emits a change event.

#### Signature

```javascript
loadXML(xml = null)
```

#### Parameters

* `xml` (String): The XML representation of the BPMN diagram (optional). If not provided, uses the currentXML.

#### Example

```javascript
await loadXML(xml);
```

### **Method**: `validateDropTarget`

Validates the drop target based on the provided client coordinates and control information.

#### Signature

```javascript
validateDropTarget({ clientX: number, clientY: number, control: Object }): void
```

#### Parameters

* `clientX`: The x-coordinate of the client position.&#x20;
* `clientY`: The y-coordinate of the client position.&#x20;
* `control`: An object containing control information.

#### Example

```javascript
validateDropTarget({ clientX: 100, clientY: 200, control: { type: 'node' } });
```

### Method: `isBpmnNode`

Checks whether the given shape is a BPMN node.

#### Signature

```javascript
isBpmnNode(shape: Object): boolean
```

#### Parameters

* `shape`: The shape object to be checked.

#### Example

```javascript
const shape = { component: { node: { isType: () => true } } };
const result = isBpmnNode(shape);
```

### Method: `setShapeStacking`

Sets the stacking order for the provided shape.

#### Signature

```javascript
setShapeStacking(shape: Object): void
```

#### Parameters

* `shape`: The shape object for which to set the stacking order.

#### Example

```javascript
const shape = { component: { node: { isType: () => false } } };
setShapeStacking(shape);
```

### Method: `showSavedNotification`

Displays a notification indicating that the changes have been saved.

#### Signature

```javascript
showSavedNotification(): void
```

#### Example

```javascript
showSavedNotification();
```

### Method: `setVersionIndicator`

Sets the version indicator based on whether the current state is a draft.

#### Signature

```javascript
setVersionIndicator(isDraft: boolean): void
```

#### Parameters

* `isDraft`: A boolean indicating whether the current state is a draft.

#### Example

```javascript
setVersionIndicator(true);
```

## Conclusion

In conclusion, developers can leverage this comprehensive reference guide to enhance their proficiency in utilizing the ProcessMaker's Modeler effectively. Hence, by understanding the functions, events, and methods, developers can unlock the full potential of the Modeler and customize the functionalities of it.
