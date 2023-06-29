---
description: This guide is meant to help developers to customize the modeler experience
---

# Adding an Element to the Modeler

## Overview

The extensibility of the ProcessMaker modeler empowers developers to create a customized modeling environment that aligns with their business processes and requirements, ultimately improving productivity and facilitating efficient process design and automation.

{% hint style="info" %}
Developers can extend the ProcessMaker modeler by adding a new component to enhance its functionality and customize the user experience. This allows developers to create unique components with their own behavior, appearance, and configuration options in the modeler.
{% endhint %}

## Example of adding a new Component

To add a new component in the Modeler, developers need to create a Vue component, a component config, and then register your component using the `registerNode` method.

### Step 1: Create the Component Config

Start by creating a component configuration file. This file defines various properties of the component, such as its unique ID, Vue component reference, BPMN type, control visibility, category, icon, label, and more. It also includes functions to define the BPMN definition and diagram objects for the component, using an instance of `bpmn-moddle`. Additionally, the configuration can specify the inspector panel's configuration, including form elements and their respective configurations.

Create your component config and save it in a `.js` file, such as `CustomComponentConfig.js`:

```javascript
// CustomComponentConfig.js

export default {
  // A unique ID that will be used to identify your component
  id: 'unique-custom-component-id',

  // A reference to the Vue component representing your component
  component: CustomComponent,

  // The BPMN type for your component, which will be used to save the component in XML
  // It should be in the form "prefix:name"
  bpmnType: 'custom-namespace:CustomComponent',

  // A toggle to show/hide the component in the controls panel
  control: true,

  // The category to place the component under in the controls panel
  category: 'BPMN',

  // The icon representing the component in the controls panel
  icon: require('@/assets/toolpanel/scriptTask.svg'),

  // The label for the component in the controls panel
  label: 'Script Task',

  // The function used to create the BPMN definition object for the component in XML
  // moddle is a reference to an instance of bpmn-moddle: https://github.com/bpmn-io/bpmn-moddle
  definition(moddle) {
    return moddle.create('bpmn:ScriptTask', {
      name: 'Script Task',
    });
  },

  // The function used to create the BPMN diagram object for the component in XML
  // moddle is a reference to an instance of bpmn-moddle: https://github.com/bpmn-io/bpmn-moddle
  diagram(moddle) {
    return moddle.create('bpmndi:BPMNShape', {
      bounds: moddle.create('dc:Bounds', {
        height: taskHeight,
        width: 116,
      }),
    });
  },

  // The configuration for the inspector panel
  inspectorConfig: [
    {
      name: 'CustomComponent',
      items: [
        // Each item corresponds to a form element.
        {
          // Component can be a custom Vue component or a reference to a form component from @processmaker/vue-form-elements
          component: 'FormText',
          config: {
            label: 'Custom Component Label',
            fontSize: '2em',
          },
        },
        // ...
      ],
    },
    // ...
  ],
};

```

### Step 2: Create the Vue Component

This component will be responsible for defining the visual representation and behavior of the custom component within the modeler. It can be based on an existing component or extend one of the pre-existing components provided by ProcessMaker. Developers have the flexibility to customize the component's appearance and add specific behavior as needed.

Create a [Vue component](https://vuejs.org/v2/guide/components.html) for your custom element, such as `CustomComponent.vue`:

```javascript
<template>
  <div />
</template>

<script>
import Task from '@/components/nodes/task/task';

export default {
  extends: Task,
  mounted() {
    // Perform any necessary operations with this.shape
  },
};
</script>
```

### Step 3: Register the Custom Component

Finally, register the custom component using the `registerNode` method provided by the ProcessMaker modeler. This step integrates the newly created component into the modeler, making it available for use. By providing the component configuration created in the first step, the modeler recognizes and adds the component with the specified ID, behavior, appearance, and configuration options.

Register your custom component using the `registerNode` method:

```javascript
registerNode(CustomComponentConfig);
```

## Conclusion

By following these steps, developers can extend the ProcessMaker modeler by adding unique components tailored to their specific requirements. These components can introduce new functionality, enhance the user experience, and provide additional configuration options through the inspector panel.
