<template>
  <div class="form-group">
    <label :for="name">{{ label }}</label>
    <component :is="tag" :name="name" :required="required">
      <option v-if="tag === 'select'" value="">Выберите {{ label }}</option>
      <option v-for="user in options" :key="user.id" :value="user.id">{{ user.name + ' - ' + user.id }}</option>
    </component>
  </div>
</template>
<script>
export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    required: {
      type: Boolean,
      default: false,
    },
    type: {
      type: String,
      default: 'text',
      validator: value => ['text', 'number'].includes(value),
    },
    options: {
      type: Array,
      default: null,
    },
  },
  computed: {
    tag () {
      return this.options ? 'select' : 'input'
    }
  },
}
</script>
