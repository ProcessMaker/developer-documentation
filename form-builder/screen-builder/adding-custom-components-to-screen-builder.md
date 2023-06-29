---
description: >-
  This guide is meant to help developers to add a new element in the screen
  builder.
---

# Adding Custom Components to Screen Builder

## Overview

ProcessMaker's Screen Builder is designed to be highly adaptable, allowing developers to create custom elements that suit their specific business needs. Therefore, developers have the power to add new elements to Screen Builder, tailoring it to their unique business requirements.&#x20;

## Adding a New Element to Screen Builder

To seamlessly incorporate a new element into Screen Builder, follow these steps.

### Step 1: Identify the Element

Identify the element you want to add. For this example, add a new component called `FormSlider`.

### Step 2: Create the FormSlider Component File

Create a new file called `form-slider.vue` inside the `components/renderer` directory. This file will contain the implementation of the `FormSlider` component.

### Step 3: Implement the `FormSlider` Component

Implement the `FormSlider` component according to your requirements. Below is an example implementation.

```html
<template>
  <div>
    <!-- Your component template goes here -->
    <input type="range" v-model="value" :min="min" :max="max" :step="step">
  </div>
</template>

<script>
export default {
  name: 'FormSlider',
  props: {
    value: {
      type: Number,
      default: 0,
    },
    min: {
      type: Number,
      default: 0,
    },
    max: {
      type: Number,
      default: 100,
    },
    step: {
      type: Number,
      default: 1,
    },
  },
};
</script>

<style scoped>
/* Your component styles go here */
</style>
```

### Step 4: Update Import Statements

Update the import statements at the top of the file to include `FormSlider`:

```javascript
import FormSlider from './components/renderer/form-slider'; // Add this line
```

### Step 5: Add `FormSlider` to the Components Array

Add a new object to the export default array, representing the `FormSlider` component:

```javascript
export default [
  // Existing components...
{
    editorComponent: FormSlider,
    editorBinding: 'FormSlider',
    rendererComponent: FormSlider,
    rendererBinding: 'FormSlider',
    control: {
      label: 'Slider',
      component: 'FormSlider',
      'editor-component': 'FormSlider',
      'editor-control': 'FormSlider',
      config: {
        // Add the configuration options for your component
        label: 'Slider',
        icon: 'fas fa-sliders-h',
      },
      inspector: [{
        type: 'FormInput',
        field: 'label',
        config: {
          label: 'Label',
          helper: 'The text to display',
        },
      },
      {
        type: 'FormInput',
        field: 'name',
        config: {
          label: 'Name',
          helper: 'Variable Name',
        },
      },
      ],
    },
  },
];

```

### Step 6: Save and Verify Component Integration

Save the file and make sure it is properly imported and added to the array of components.

### Step 7: Using the `FormSlider` Component in the Screen Builder

You can now use the `FormSlider` component in Screen Builder by selecting it from the component list. Customize the configuration options and inspector properties as needed for your components.
