<template>
  <div class="modal">

    <div class="modal-overlay"></div>

    <div class="modal-container">
      <div class="modal-header">
        <h3>Новый пользователь</h3>
        <button @click="closeModal()" class="modal-close-button">
          &times;
        </button>
      </div>

      <div class="modal-body">
        <form-component :users="users"></form-component>
      </div>
    </div>

  </div>
</template>

<script>
import FormComponent from './AddUserForm.vue'

export default {
  props: {
    users: {
      type: Array,
      required: true,
    },
  },

  components: {
    FormComponent,
  },

  methods: {
    closeModal () {
      this.$emit('closeModal')
    },

  },
}
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-container {
  position: relative;
  width: auto;
  max-width: 100%;
  background-color: #fff;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
}

.modal-header {
  padding: 20px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-body {
  padding: 20px;
}

.modal-close-button {
  border: none;
  background-color: transparent;
  font-size: 30px;
  cursor: pointer;
}
</style>
