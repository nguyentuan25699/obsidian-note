## I. VueJS
---
- Vue is a framework for building UI components, like React, but it uses a more HTML-like style of writing.
- A Vue file is usually a Single File Component, which contains three parts: 

```vue
<script setup lang="ts">
const message = 'Hello Vue'
</script>

<template>
  <h1>{{ message }}</h1>
</template>

<style scoped>
h1 {
  color: green;
}
</style>
```

- Comparison with React: 

| **React**      | **Vue**          | **VI**                        |
| -------------- | ---------------- | ----------------------------- |
| useState       | ref, reactive    | Quản lý state                 |
| useMemo        | computed         | Tính giá trị phụ thuộc state  |
| useEffect      | watch, onMounted | Side effect / lifecycle       |
| props          | defineProps      | Truyền dữ liệu cha → con      |
| callback props | defineEmits      | Bắn event con → cha           |
| children       | slot             | Nội dung truyền vào component |
| React Router   | Vue Router       | Điều hướng page               |
| Zustand/Redux  | Pinia            | Global state                  |

Vue 3 commonly uses the Composition API, which means writing logic with functions like **`ref()`**, **`computed()`**, **`watch()`**, and **`onMounted()`**, instead of separating logic into options like **data**, **methods**, and **computed** as in the old **Options API**.

#### 1. Structure of a .vue file
```vue 
<script setup lang="ts">
/**
 * Logic goes here
 */
</script>

<template>
  <!-- UI goes here -->
</template>

<style scoped>
/* Styles go here */
</style>
```

| **Section**     |                                    |
| --------------- | ---------------------------------- |
| \<script setup> | Where you write JS/TS logic        |
| \<template>     | Where you write UI                 |
| \<style scoped> | CSS only applies to this component |

## II. Vue syntax
---
#### 1. Syntax on Vue component
```vue
<script setup lang="ts">
import { ref, computed } from 'vue'

const count = ref(0)

const doubleCount = computed(() => count.value * 2)

function increase() {
  count.value++
}
</script>

<template>
  <div>
    <p>Count: {{ count }}</p>
    <p>Double: {{ doubleCount }}</p>
    <button @click="increase">+</button>
  </div>
</template>
```

- Point: 
```vue
const count = ref(0)
count.value++
```
- In \<script>, we use .value
- But in \<template>, Vue automatically unwraps refs, so we can just write it like this:
  ```vue
  {{ count }}
  ```

#### 2. Binding on template
- The most commonly used syntax: 
```vue 
<!-- render text -->
<p>{{ userName }}</p>

<!-- bind attribute -->
<img :src="avatarUrl" />

<!-- event -->
<button @click="handleClick">Save</button>

<!-- conditional render -->
<p v-if="isLoading">Loading...</p>
<p v-else>Done</p>

<!-- loop -->
<div v-for="item in items" :key="item.id">
  {{ item.name }}
</div>

<!-- two-way binding -->
<input v-model="keyword" />
```


 - Quick map:

| **Vue**     | **Means**                               |
| ----------- | --------------------------------------- |
| :src="url"  | bind attribute, like src={url} in React |
| @click="fn" | event, like onClick={fn}                |
| v-if        | conditional render                      |
| v-for       | loop                                    |
| v-model     | two-way binding form input              |

#### 3. Props and Emit
- Child component:
```vue 
<script setup lang="ts">
type Props = {
  title: string
  count?: number
}

defineProps<Props>()

const emit = defineEmits<{
  save: [value: string]
}>()

function handleSave() {
  emit('save', 'hello')
}
</script>

<template>
  <div>
    <h2>{{ title }}</h2>
    <button @click="handleSave">Save</button>
  </div>
</template>
```

- Parent component:
```vue 
<ChildComponent
  title="Demo"
  :count="10"
  @save="handleSave"
/>
```


## III. Learing
#### 1. Component, State, Template
- State with ref: `ref` is used to create reactive state for simple values like string, number, and boolean.
```vue
<script setup lang="ts">
import { ref } from 'vue'

const count = ref(0)

function increase() {
  count.value++
}
</script>

<template>
  <div>
    <p>Count: {{ count }}</p>
    <button @click="increase">Increase</button>
  </div>
</template>
```

- State with reactive: `reactive` is usually used for objects or form data.
```vue 
<script setup lang="ts">
import { reactive } from 'vue'

const form = reactive({
  email: '',
  password: '',
})

function submitForm() {
  console.log(form.email, form.password)
}
</script>

<template>
  <input v-model="form.email" placeholder="Email" />
  <input v-model="form.password" placeholder="Password" />
  <button @click="submitForm">Submit</button>
</template>
```

#### 2. Template Syntax
- Text interpolation
```vue 
<p>{{ userName }}</p>
```
Render a variable value to the UI.

- Attribute binding
```vue 
<img :src="avatarUrl" />
```
The : symbol is used to bind dynamic values.

- Event binding
```vue 
<button @click="handleClick">Save</button>
```
The `@` symbol is used to listen to events.

- Conditional rendering
```vue 
<p v-if="isLoading">Loading...</p>
<p v-else>Done</p>
```
`v-if` is similar to `{condition && ...}` or ternary rendering in React.

- List rendering
```vue 
<div v-for="item in items" :key="item.id">
  {{ item.name }}
</div>
```
`v-for` is similar to `.map()` in React.

- Two-way binding with v-model
```vue 
<input v-model="keyword" />
```
`v-model` automatically binds the input value and updates state when the input changes.

#### 3. Props, Emits, Slots
